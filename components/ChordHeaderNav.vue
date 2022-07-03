<template>
  <div v-if="chordsheet" class="header header-fixed header-logo-center">
    <div class="header-title">{{ chordsheet.song_name }}</div>
    <NuxtLink to="/search" class="header-icon header-icon-1"
      ><i class="fas fa-arrow-left"></i
    ></NuxtLink>
    <a
      href="#"
      @click="toogleeditor"
      data-toggle-theme
      class="header-icon header-icon-4"
    >
      <i v-if="!editor" class="fas fa-pen"></i>
      <i v-if="editor" class="fas fa-check"></i>
    </a>
  </div>
</template>
<script setup>
import axios from "axios";
const loading = useLoadingScreen();
const editor = useEditor();
const chordsheet = useChordSheet();

function toogleeditor() {
  if (editor.value) editordone();

  editor.value = !editor.value;
}

async function editordone() {
  loading.value = true;
  if (process.client) {
    const reqbody = {
      text: document.getElementById("chordsheeteditor").value,
    };
    const result = await axios.post(
      "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/texttochordsheet",
      reqbody
    );
    chordsheet.value.transposedchordsheet = "";
    chordsheet.value.chordsheet = result.data.body;
  }
  loading.value = false;
}
</script>

<style scoped>
.header-title {
  overflow: hidden;
}
</style>
