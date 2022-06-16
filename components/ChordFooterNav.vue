<template>
  <div>
    <div class="chordfooter">
      <div data-menu="menu-settings"><i class="fa fa-cog"></i></div>
    </div>

    <div id="menu-settings" class="menu menu-box-bottom menu-box-detached">
      <div class="menu-title mt-0 pt-0">
        <h1>Settings</h1>
        <!-- <p class="color-highlight">Flexible and Easy to Use</p> -->
        <a href="#" class="close-menu"><i class="fa fa-times"></i></a>
      </div>
      <div class="divider divider-margins mb-n2"></div>
      <div class="content mb-0">
        <div class="d-flex mb-4">
          <div class="d-flex">
            <i
              class="fa font-12 fa-music rounded-s bg-highlight color-white me-3 customi"
            ></i>
            <span>轉</span>
            <span>調</span>
          </div>
          <div class="ms-3 w-100">
            <div class="stepper rounded-s scale-switch ms-n1 float-end">
              <a @click="transposedown" class="stepper-sub"
                ><i class="fa fa-minus color-theme opacity-40"></i
              ></a>
              <input
                type="number"
                min="-11"
                max="11"
                v-model="chordsheet.transpose"
                @change="transposechordsheet"
              />
              <a @click="transposeup" class="stepper-add"
                ><i class="fa fa-plus color-theme opacity-40"></i
              ></a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const chordsheet = useChordSheet();
import { chordParserFactory, chordRendererFactory } from "chord-symbol";
import * as ChordParser from "chord-parser";
const parseChord = chordParserFactory();

async function transposedown() {
  if (chordsheet.value.transpose < -10) return;
  chordsheet.value.transpose--;
  transposechordsheet();
}

async function transposeup() {
  if (chordsheet.value.transpose > 10) return;
  chordsheet.value.transpose++;
  transposechordsheet();
}

async function transposechordsheet() {
  chordsheet.value.transposedchordsheet = chordsheet.value.chordsheet.map(
    (x) => {
      const chordline = x.chord;

      if (chordline) {
        var tabs = new ChordParser(chordline);

        let allchords = [];
        let chordindex = [];
        let nowindex = 0;
        tabs.wrap(function (chord) {
          const tempstartindex = chordline.indexOf(chord, nowindex);
          nowindex = tempstartindex;
          chordindex.push({
            start: tempstartindex,
            end: tempstartindex + chord.length,
          });
          const normoalizedchord = parseChord(chord);
          const renderChord = chordRendererFactory({
            useShortNamings: true,
            transposeValue: chordsheet.value.transpose,
          });
          allchords.push(renderChord(normoalizedchord));
        });

        const normoalizedchordline = allchords.join(" ");

        if (normoalizedchordline) {
          let transposedchords = [];

          console.log(transposedchords);
          let transposedchordline = "";

          chordindex.map((y, ind) => {
            transposedchordline +=
              chordline.slice(ind ? chordindex[ind - 1].end : 0, y.start) +
              allchords[ind];
          });
          transposedchordline += chordline.slice(
            chordindex[chordindex.length - 1].end
          );

          return {
            lyric: x.lyric,
            chord: transposedchordline,
          };
        }
      }
      return "";
    }
  );
}
</script>

<style scoped>
.customi {
  width: 30px;
  height: 30px;
  line-height: 30px;
  /* margin-top: 10px; */
  text-align: center;
  float: left;
}

.chordfooter {
  position: fixed;
  bottom: 5px;
  right: 5px;
  z-index: 999;
  font-size: 28px;
  color: #ab9103;
  opacity: 0.8;
}
</style>
