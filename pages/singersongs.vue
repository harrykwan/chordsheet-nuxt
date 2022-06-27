<template>
  <div>
    <div class="header header-fixed header-logo-center">
      <div class="header-title">歌曲列表</div>
      <div @click="goback" class="header-icon header-icon-1">
        <i class="fas fa-arrow-left"></i>
      </div>
      <!-- <a href="#" data-toggle-theme class="header-icon header-icon-4"
      ><i class="fas fa-pen"></i
    ></a> -->
    </div>
    <SingerSongList />
  </div>
</template>

<script setup>
const router = useRouter();
function goback() {
  router.back();
}
</script>
