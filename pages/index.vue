<template>
  <div>
    <FooterNav />
    <div class="header header-fixed header-logo-center header-auto-show">
      <a href="index.html" class="header-title">揾Chord</a>
      <!-- <a href="#" data-back-button class="header-icon header-icon-1"
        ><i class="fas fa-arrow-left"></i
      ></a>
      <a href="#" data-toggle-theme class="header-icon header-icon-4"
        ><i class="fas fa-lightbulb"></i
      ></a> -->
    </div>
    <div class="page-content header-clear-small">
      <div class="content mt-0 mb-4">
        <div class="d-flex">
          <div class="align-self-center me-auto">
            <strong class="text-uppercase opacity-60 font-12"
              >Let's Play Some Songs</strong
            >
            <h1 class="mt-n2 font-28">揾Chord</h1>
          </div>
          <div class="align-self-center ms-auto mt-1">
            <a href="#" class="d-block"
              ><img
                src="images/fitness/2t.jpg"
                class="img-fluid shadow-xl rounded-circle"
                width="52"
                alt="img"
            /></a>
          </div>
        </div>
      </div>

      <div
        class="card card-style"
        data-card-height="170"
        style="background-image: url(images/fitness/14m.jpg)"
      >
        <div class="card-top p-2">
          <!-- <a
            href="#"
            class="btn btn-xs bg-white color-black font-700 text-uppercase rounded-s"
            >Start</a
          > -->
        </div>

        <div class="card-bottom p-3">
          <h1 class="color-white mb-n1">男歌手</h1>
          <p class="color-white mb-0 opacity-60">Click Me</p>
        </div>
        <div class="card-overlay bg-gradient"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
const loading = useLoadingScreen();
loading.value = true;
onMounted(() => {
  if (process.client) {
    setTimeout(() => {
      try {
        init_template();
        loading.value = false;
      } catch (e) {
        console.log(e);
        loading.value = false;
      }
    }, 100);
  }
});
</script>
