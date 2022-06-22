<template>
  <div>
    <FooterNav />
    <div class="header header-fixed header-logo-center header-auto-show">
      <a href="index.html" class="header-title">
        <img class="toplogo" :src="'/images/buskking-yellow.png'" />
        <span>BUSKKING</span></a
      >

      <!-- <a href="#" data-back-button class="header-icon header-icon-1"
        ><i class="fas fa-arrow-left"></i
      ></a>
      <a href="#" data-toggle-theme class="header-icon header-icon-4"
        ><i class="fas fa-lightbulb"></i
      ></a> -->
    </div>

    <div class="page-content header-clear pb-3">
      <div
        class="card position-fixed w-100"
        data-card-height="400"
        style="
          background: none;
          background-image: url('images/guitar.jpg');
          margin-top: -50px;
        "
      >
        <div
          :class="{
            biglogocontainer_black: theme == 'dark',
            biglogocontainer_white: theme == 'light',
          }"
        >
          <img
            class="biglogo brightness"
            :src="'/images/buskking-yellow.png'"
          />
        </div>

        <div class="card-bottom disabled mb-5 pb-3 mt-2 text-center">
          <a
            href="#"
            data-menu="menu-share"
            class="mx-2 icon icon-xs rounded-s bg-blue2-dark"
            ><i class="fa fa-share-alt"></i
          ></a>
          <a
            href="#"
            data-menu="menu-share"
            class="mx-2 icon icon-xs rounded-s bg-red2-dark"
            ><i class="fa fa-bookmark"></i
          ></a>
        </div>
        <div class="card-top mb-5 pb-3 mt-2 text-center"></div>
        <div class="card-overlay bg-gradient opacity-10"></div>
      </div>
      <div
        class="card border-0 shadow-0 bg-transparent no-click"
        data-card-height="320"
      ></div>

      <div class="card card-style mx-0 mb-0 pb-5">
        <div
          class="divider mx-auto mt-3 bg-gray-dark opacity-30 rounded-s mb-n1"
          style="height: 5px; width: 50px"
        ></div>
        <div class="content">
          <div
            class="card card-style bg-28"
            style="background-image: url('images/perform.webp')"
          >
            <div class="card-body my-3">
              <h1 class="color-white">WHY ME</h1>
              <p class="color-white opacity-60 mb-0">
                揾譜？執譜？學音樂？依度可以一次過滿足你。升降Key、學 guitar tab
                冇廣告、唔使登入!
              </p>
              <NuxtLink
                to="/search"
                class="btn btn-s rounded-sm bg-highlight color-white mt-3 text-uppercase font-800"
                ><i class="fa fa-play-circle pe-2"></i>即刻試下</NuxtLink
              >
            </div>
            <div class="card-overlay bg-black opacity-50"></div>
          </div>

          <div class="divider divider-margins"></div>

          <!-- <div class="d-flex">
            <div class="me-auto">
              <span
                class="badge no-click bg-green-dark p-2 text-uppercase rounded-s mb-3"
                >VACATION</span
              >
            </div>
            <div class="mx-auto">
              <span class="opacity-50 font-12"
                ><i class="far fa-calendar-alt pe-2"></i>21st Aug - 28 Aug</span
              >
            </div>
            <div class="mx-auto">
              <span class="opacity-50 font-12"
                ><i class="far fa-heart pe-2"></i>25k</span
              >
            </div>
          </div> -->
          <!-- <h1 class="font-24 line-height-m pb-1">Maldives Summer Holliday</h1>
          <p class="pt-1">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur
            aliquam non nunc quis maximus. Fusce volutpat arcu id ante maximus
            vestibulum. Curabitur non nisi venenatis, pharetra nisl et,
            ullamcorper diam. Morbi interdum varius molestie. Quisque feugiat
            augue id diam ornare auctor.
          </p> -->

          <div
            class="card card-style"
            data-card-height="170"
            style="background-image: url(images/male.jpg)"
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

          <div
            class="card card-style"
            data-card-height="170"
            style="background-image: url(images/female.jpg)"
          >
            <div class="card-top p-2">
              <!-- <a
            href="#"
            class="btn btn-xs bg-white color-black font-700 text-uppercase rounded-s"
            >Start</a
          > -->
            </div>

            <div class="card-bottom p-3">
              <h1 class="color-white mb-n1">女歌手</h1>
              <p class="color-white mb-0 opacity-60">Click Me</p>
            </div>
            <div class="card-overlay bg-gradient"></div>
          </div>

          <div
            class="card card-style"
            data-card-height="170"
            style="background-image: url(images/tgt.jpg)"
          >
            <div class="card-top p-2">
              <!-- <a
            href="#"
            class="btn btn-xs bg-white color-black font-700 text-uppercase rounded-s"
            >Start</a
          > -->
            </div>

            <div class="card-bottom p-3">
              <h1 class="color-white mb-n1">組合</h1>
              <p class="color-white mb-0 opacity-60">Click Me</p>
            </div>
            <div class="card-overlay bg-gradient"></div>
          </div>
        </div>

        <div class="divider divider-margins" hidden></div>

        <div
          hidden
          class="card card-style bg-17"
          data-card-height="400"
          style="background-image: url('images/travel/4m.jpg')"
        >
          <div class="card-center text-center">
            <h2 class="color-white pt-2">"Something I'll never forget"</h2>
            <a href="#" class="color-white">Jack Son - Tourist</a>
          </div>
          <div class="card-overlay bg-black opacity-60"></div>
        </div>

        <div class="divider divider-margins" hidden></div>

        <div class="content mt-0" hidden>
          <h4>This is an Image Gallery</h4>
          <p>
            This page is not WordPress, it's an HTML website. Yes, that's right.
            but you can convert it to WordPress yourself or hire an expert from
            Envato Studio.
          </p>
          <div class="row mb-0">
            <div class="col-4">
              <a
                href="images/travel/1m.jpg"
                class="default-link"
                data-gallery="gallery-1"
                title="Image Title or Caption"
              >
                <img
                  :src="'images/empty.png'"
                  data-src="images/travel/1s.jpg"
                  class="preload-img shadow-s img-fluid rounded-s"
                  alt="img"
                />
              </a>
            </div>
            <div class="col-4">
              <a
                href="images/travel/4m.jpg"
                class="default-link"
                data-gallery="gallery-1"
                title="Image Title or Caption"
              >
                <img
                  :src="'images/empty.png'"
                  data-src="images/travel/4s.jpg"
                  class="preload-img shadow-s img-fluid rounded-s"
                  alt="img"
                />
              </a>
            </div>
            <div class="col-4">
              <a
                href="images/travel/8m.jpg"
                class="default-link"
                data-gallery="gallery-1"
                title="Image Title or Caption"
              >
                <img
                  :src="'images/empty.png'"
                  data-src="images/travel/8s.jpg"
                  class="preload-img shadow-s img-fluid rounded-s"
                  alt="img"
                />
              </a>
            </div>
          </div>
        </div>

        <div class="divider divider-margins" hidden></div>

        <FooterNotes />
      </div>
    </div>
  </div>
</template>

<script setup>
const loading = useLoadingScreen();
const theme = useTheme();
loading.value = true;

function initpage() {
  if (process.client) {
    setTimeout(() => {
      try {
        init_template();
        loading.value = false;
      } catch (e) {
        console.log(e);
        alert(e);
        loading.value = false;
      }
    }, 100);
  }
}

onMounted(() => {
  initpage();
});
</script>

<style scoped>
.toplogo {
  width: 80px;
  margin-top: -18px;
  height: 54px;
  object-fit: cover;
  object-position: top;
  padding-top: 10px;
  margin-right: -15px;
}

.header-title {
  margin-left: -85px;
}

@-webkit-keyframes brightness {
  0%,
  100% {
    -webkit-filter: brightness(120%);
  }
  50% {
    -webkit-filter: brightness(120%) saturate(2) drop-shadow(5px 5px 10px #aaa);
  }
}

.brightness {
  -webkit-animation: brightness 3s infinite;
}

.biglogo {
  position: inherit;
  width: 300px;
  /* height: 300px;
  object-fit: cover; */
  /* backdrop-filter: blur(10px); */
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  margin-top: 30px;
  border: 0px solid black;
  border-radius: 50%;
  /* background: black; */
  filter: brightness(120%);
}

.biglogocontainer_black {
  width: 100%;
  height: 100%;
  position: inherit;
  background: linear-gradient(
    to top,
    rgba(0, 0, 0, 0) 0%,
    rgba(0, 0, 0, 0.5) 20%,
    rgba(0, 0, 0, 0.7) 30%,
    rgba(0, 0, 0, 0.8) 70%,
    rgba(0, 0, 0, 0.8) 100%
  ) !important;

  backdrop-filter: blur(2px);
}

.biglogocontainer_white {
  width: 100%;
  height: 100%;
  position: inherit;
  background: linear-gradient(
    to top,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.5) 20%,
    rgba(255, 255, 255, 0.7) 30%,
    rgba(255, 255, 255, 0.8) 70%,
    rgba(255, 255, 255, 0.8) 100%
  ) !important;

  backdrop-filter: blur(2px);
}
</style>
