<template>
  <div>
    <div id="footer-bar" class="footer-bar-1">
      <NuxtLink to="/" :class="{ 'active-nav': pagenum == 1 }"
        ><i class="fa fa-home"></i><span>介紹</span></NuxtLink
      >
      <NuxtLink :class="{ 'active-nav': pagenum == 2 }"
        ><i class="fa fa-star"></i><span>潮流</span></NuxtLink
      >
      <NuxtLink :class="{ 'active-nav': pagenum == 3 }"
        ><i class="fa fa-heart"></i><span>已存</span></NuxtLink
      >
      <NuxtLink :class="{ 'active-nav': pagenum == 4 }" to="/search"
        ><i class="fa fa-search"></i><span>揾譜</span></NuxtLink
      >
      <NuxtLink href="#" data-menu="menu-settings"
        ><i class="fa fa-cog"></i><span>設定</span></NuxtLink
      >
    </div>
    <div id="menu-settings" class="menu menu-box-bottom menu-box-detached">
      <div class="menu-title mt-0 pt-0">
        <h1>Settings</h1>

        <a href="#" class="close-menu"><i class="fa fa-times"></i></a>
      </div>
      <div class="divider divider-margins mb-n2"></div>
      <div class="content">
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
        <div class="list-group list-custom-large">
          <a data-menu="menu-highlights" href="#">
            <i class="fa font-14 fa-tint bg-green-dark rounded-s"></i>
            <span>Page Highlight</span>
            <strong>16 Colors Highlights Included</strong>
            <span class="badge bg-highlight color-white">HOT</span>
            <i class="fa fa-angle-right"></i>
          </a>
          <a data-menu="menu-backgrounds" href="#" class="border-0">
            <i class="fa font-14 fa-cog bg-blue-dark rounded-s"></i>
            <span>Background Color</span>
            <strong>10 Page Gradients Included</strong>
            <span class="badge bg-highlight color-white">NEW</span>
            <i class="fa fa-angle-right"></i>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const pagesetting = usePageSetting();
const theme = useTheme();
const pagenum = ref(1);
const route = useRoute();

coloricon();

watch(route, () => {
  coloricon();
});

function coloricon() {
  if (route.path == "/") {
    pagenum.value = 1;
  } else if (route.path.indexOf("search") != -1) {
    pagenum.value = 4;
  }
}

function toggletheme() {
  if (theme.value == "dark") theme.value = "light";
  else theme.value = "dark";
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
</style>
