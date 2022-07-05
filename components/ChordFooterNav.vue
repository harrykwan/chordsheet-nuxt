<template>
  <div>
    <div class="chordfooter" :hidden="editor">
      <div class="mb-3"><i class="fa fa-play"></i></div>
      <div class="mb-3" @click="savenewsheet"><i class="fa fa-save"></i></div>
      <div data-menu="menu-settings"><i class="fa fa-cog"></i></div>
    </div>

    <div id="menu-settings" class="menu menu-box-bottom">
      <div class="menu-title mt-0 pt-0">
        <h1>Settings</h1>

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
            <span>歌詞</span>
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
        <div class="list-group list-custom-small">
          <a
            href="#"
            data-toggle-theme
            data-trigger-switch="switch-dark-mode"
            class="pb-2 ms-n1"
          >
            <i
              class="fa font-12 fa-moon rounded-s bg-highlight color-white me-3"
            ></i>
            <span>Dark Mode</span>
            <div
              class="custom-control scale-switch ios-switch"
              @click="toggletheme"
            >
              <input
                type="checkbox"
                class="ios-input"
                id="switch-dark-mode"
                :checked="theme == 'dark'"
              />
              <label
                class="custom-control-label"
                for="switch-dark-mode"
              ></label>
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
const editor = useEditor();
const fontsize = useFontSize();
const theme = useTheme();
const chordsheetid = useChordSheetId();

function toggletheme() {
  if (theme.value == "dark") theme.value = "light";
  else theme.value = "dark";
}

function appendnewsheet(id) {
  if (process.client) {
    let nowlist = [];

    try {
      JSON.parse(localStorage.getItem("chordsheetlist"));
    } catch (e) {}
    nowlist.push(id);
    localStorage.setItem("chordsheetlist", JSON.stringify(nowlist));
  }
}

function savenewsheet() {
  if (process.client) {
    let nowsheetid = "";
    if (chordsheetid.value) nowsheetid = chordsheetid.value;
    else {
      nowsheetid = uuidv4();
      appendnewsheet(nowsheetid);
    }
    const tempdata = {
      updatetime: Date.now(),
      chordsheet: chordsheet.value,
    };
    localStorage.setItem(nowsheetid, JSON.stringify(tempdata));
  }
}

function uuidv4() {
  return ([1e7] + -1e3 + -4e3 + -8e3 + -1e11).replace(/[018]/g, (c) =>
    (
      c ^
      (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))
    ).toString(16)
  );
}

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
  console.log(reqbody);
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
}

.chordfooter > div {
  opacity: 0.4;
}

.chordfooter > div:hover {
  opacity: 1;
  cursor: pointer;
}
</style>
