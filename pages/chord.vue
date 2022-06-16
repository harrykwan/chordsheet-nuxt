<template>
  <div>
    <ChordFooterNav />
    <ChordHeaderNav />
    <div id="page" v-if="chordsheet">
      <div class="page-content header-clear-medium">
        <!--
			How to find your preferred action sheet fast and easy in this large page:

			For example, if you want to use the data-menu="menu-call" actionsheet please use CTRL+F or CMD+F
			and search for id="menu-call". This is the easiest way to locate your preferred action sheet.
		-->

        <div class="card card-style">
          <div class="content">
            <!-- <h1 class="font-21">song name</h1> -->
            <!-- <p class="color-highlight font-12 mt-n3 pt-1 mb-2">artist name</p> -->
            <div
              class="mb-3"
              v-for="(item, ind) in chordsheet.transposedchordsheet
                ? chordsheet.transposedchordsheet
                : chordsheet.chordsheet"
              :key="ind"
            >
              <div class="color-white">
                <pre class="chord">{{ item.chord }}</pre>
              </div>
              <div>
                <pre class="lyric">{{ item.lyric }}</pre>
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
  font-size: 13px;
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
