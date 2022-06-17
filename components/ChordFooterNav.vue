<template>
  <div>
    <div class="chordfooter">
      <div data-menu="menu-settings"><i class="fa fa-cog"></i></div>
    </div>

    <div id="menu-settings" class="menu menu-box-bottom">
      <div class="menu-title mt-0 pt-0">
        <h1>Settings</h1>
        <!-- <p class="color-highlight">Flexible and Easy to Use</p> -->
        <a href="#" class="close-menu"><i class="fa fa-times"></i></a>
      </div>
      <div class="divider divider-margins mb-n2"></div>
      <div class="content mb-0">
        <div class="d-flex mb-2">
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
        <div class="divider divider-margins mb-n2"></div>
      </div>
      <div class="divider divider-margins mb-n2"></div>
      <div class="content mb-0">
        <div class="d-flex mb-2">
          <div class="d-flex">
            <i
              class="fa font-12 fa-music rounded-s bg-highlight color-white me-3 customi"
            ></i>
            <span>字</span>
            <span>體</span>
          </div>
          <div class="ms-3 w-100">
            <div class="stepper rounded-s scale-switch ms-n1 float-end">
              <a @click="fontdown" class="stepper-sub"
                ><i class="fa fa-minus color-theme opacity-40"></i
              ></a>
              <input type="number" min="-11" max="11" v-model="fontsize" />
              <a @click="fontup" class="stepper-add"
                ><i class="fa fa-plus color-theme opacity-40"></i
              ></a>
            </div>
          </div>
        </div>
        <div class="divider divider-margins mb-n2"></div>
      </div>
      <div class="content">
        <div class="list-group list-custom-small">
          <a class="pb-2 ms-n1">
            <i
              class="fa font-12 fa-moon rounded-s bg-highlight color-white me-3"
            ></i>
            <span>Chord</span>
            <div
              class="custom-control scale-switch ios-switch"
              @click="togglechord"
            >
              <input
                type="checkbox"
                class="ios-input"
                id="switch-dark-mode"
                :checked="chordshow"
              />
              <label class="custom-control-label"></label>
            </div>
            <i class="fa fa-angle-right"></i>
          </a>
        </div>
        <div class="list-group list-custom-small">
          <a class="pb-2 ms-n1">
            <i
              class="fa font-12 fa-moon rounded-s bg-highlight color-white me-3"
            ></i>
            <span>Lyrics</span>
            <div
              class="custom-control scale-switch ios-switch"
              @click="togglelyric"
            >
              <input
                type="checkbox"
                class="ios-input"
                id="switch-dark-mode"
                :checked="lyricshow"
              />
              <label class="custom-control-label"></label>
            </div>
            <i class="fa fa-angle-right"></i>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
const chordsheet = useChordSheet();
const lyricshow = useLyricShow();
const chordshow = useChordShow();
const fontsize = useFontSize();

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

async function fontup() {
  fontsize.value++;
}

async function fontdown() {
  if (fontsize.value > 1) fontsize.value--;
}

async function transposechordsheet() {
  const nowchordsheet = JSON.parse(JSON.stringify(chordsheet.value));
  const reqbody = {
    chordsheet: nowchordsheet.chordsheet,
    transpose: nowchordsheet.transpose,
  };
  const result = await axios.post(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/transposechordsheet",
    reqbody
  );
  chordsheet.value.transposedchordsheet = result.data.body;
}

async function togglelyric() {
  lyricshow.value = !lyricshow.value;
}

async function togglechord() {
  chordshow.value = !chordshow.value;
}
</script>

<style scoped>
.customi {
  width: 30px;
  height: 30px;
  line-height: 30px;
  text-align: center;
  float: left;
}

.chordfooter {
  position: fixed;
  bottom: 10px;
  right: 10px;
  z-index: 10;
  font-size: 35px;
  color: #ab9103;
  opacity: 0.8;
}
</style>
