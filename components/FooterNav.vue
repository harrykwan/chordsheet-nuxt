<template>
  <div>
    <div id="footer-bar" class="footer-bar-1">
      <NuxtLink to="/" class="active-nav"
        ><i class="fa fa-home"></i><span>介紹</span></NuxtLink
      >
      <NuxtLink><i class="fa fa-star"></i><span>潮流</span></NuxtLink>
      <NuxtLink><i class="fa fa-heart"></i><span>已存</span></NuxtLink>
      <NuxtLink to="/search"
        ><i class="fa fa-search"></i><span>揾譜</span></NuxtLink
      >
      <NuxtLink href="#" data-menu="menu-settings"
        ><i class="fa fa-cog"></i><span>設定</span></NuxtLink
      >
    </div>
    <div id="menu-settings" class="menu menu-box-bottom menu-box-detached">
      <div class="menu-title mt-0 pt-0">
        <h1>Settings</h1>
        <!-- <p class="color-highlight">Flexible and Easy to Use</p> -->
        <a href="#" class="close-menu"><i class="fa fa-times"></i></a>
      </div>
      <div class="divider divider-margins mb-n2"></div>
      <div class="content mb-0">
        <div class="d-flex mb-4">
          <div class="d-flex">
            <i
              class="fa font-12 fa-music rounded-s bg-highlight color-white me-3 customi"
            ></i>
            <span>轉</span>
            <span>調</span>
          </div>
          <div class="ms-3 w-100">
            <div class="stepper rounded-s scale-switch ms-n1 float-end">
              <a href="#" class="stepper-sub"
                ><i class="fa fa-minus color-theme opacity-40"></i
              ></a>
              <input type="number" min="-11" max="11" value="0" />
              <a href="#" class="stepper-add"
                ><i class="fa fa-plus color-theme opacity-40"></i
              ></a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const pagesetting = usePageSetting();
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
