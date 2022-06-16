<template>
  <div v-if="chordsheet" class="header header-fixed header-logo-center">
    <div class="header-title">{{ chordsheet.song_name }}</div>
    <NuxtLink to="/search" class="header-icon header-icon-1"
      ><i class="fas fa-arrow-left"></i
    ></NuxtLink>
    <a href="#" data-toggle-theme class="header-icon header-icon-4"
      ><i class="fas fa-pen"></i
    ></a>
  </div>
</template>
<script setup>
const chordsheet = useChordSheet();
</script>
