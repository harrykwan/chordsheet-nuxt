<template>
  <div>
    <ChordFooterNav />
    <ChordHeaderNav />
    <div id="page" v-if="chordsheet">
      <div class="page-content header-clear-medium">
        <div class="card card-style">
          <div class="content">
            <div
              class="mb-3"
              v-for="(item, ind) in chordsheet.transposedchordsheet
                ? chordsheet.transposedchordsheet
                : chordsheet.chordsheet"
              :key="ind"
            >
              <div
                :class="{
                  'color-white': theme == 'dark',
                  'color-black': theme == 'light',
                }"
                v-if="chordshow"
              >
                <pre :style="'font-size: ' + fontsize + 'px;'" class="chord">{{
                  item.chord
                }}</pre>
              </div>
              <div v-if="lyricshow">
                <pre :style="'font-size: ' + fontsize + 'px;'" class="lyric">{{
                  item.lyric
                }}</pre>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const loading = useLoadingScreen();
const chordsheet = useChordSheet();
const lyricshow = useLyricShow();
const chordshow = useChordShow();
const fontsize = useFontSize();
const theme = useTheme();
console.log(chordsheet.value);
loading.value = false;

onMounted(() => {
  if (!chordsheet.value) {
    navigateTo("/search");
  }
  if (process.client) {
    try {
      window.scrollTo(0, 0);
      setTimeout(() => {
        init_template();
        loading.value = false;
      }, 100);
    } catch (e) {
      console.log(e);
    }
  }
});
</script>

<style scoped>
.chord,
.lyric {
  font-family: "Segoe UI", Arial, sans-serif;
}
pre {
  white-space: pre-wrap; /* Since CSS 2.1 */
  white-space: -moz-pre-wrap; /* Mozilla, since 1999 */
  white-space: -pre-wrap; /* Opera 4-6 */
  white-space: -o-pre-wrap; /* Opera 7 */
  word-wrap: break-word; /* Internet Explorer 5.5+ */
  margin-top: 0px;
  margin-bottom: 0px;
}
</style>
