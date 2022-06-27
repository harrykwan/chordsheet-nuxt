<template>
  <div style="margin-top: 40px" id="page">
    <div class="page-content header-clear-small">
      <div class="card card-style">
        <div class="content">
          <div class="search-box search-header bg-theme card-style me-3 ms-3">
            <i class="fa fa-search"></i>
            <input
              type="text"
              class="border-0"
              placeholder="揾緊邊首歌？"
              v-model="searchinput"
            />
            <a href="#" class="clear-search disabled mt-0"
              ><i class="fa fa-times color-red-dark"></i
            ></a>
          </div>

          <div
            class="search-no-results"
            v-if="showresult.length == 0 && !smallloading"
          >
            <h3 class="bold top-10">暫時沒有這歌手歌曲的資料</h3>
            <span class="under-heading font-11 opacity-70 color-theme"
              >請試試其他關鍵字眼</span
            >
          </div>

          <div
            class="search-trending card card-style"
            v-if="showresult.length > 0 || smallloading"
          >
            <div class="content mb-2">
              <h3>{{ route.hash }}</h3>
              <p class="font-11 mt-n2"></p>
            </div>

            <div v-if="smallloading" class="mt-2 mb-2">
              <div class="content">
                <div class="d-flex justify-content-center">
                  <div
                    class="spinner-border color-red-dark"
                    role="status"
                  ></div>
                </div>
              </div>
            </div>
            <div class="list-group list-custom-small me-3 ms-3">
              <a
                @click="choosesinger(item)"
                href="#"
                v-for="(item, ind) in showresult"
                :key="ind"
              >
                <span class="font-400"> {{ item }} </span>
                <i class="color-gray-dark fa fa-angle-right"></i>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const loading = useLoadingScreen();
const smallloading = ref(false);
const searchinput = ref("");
const showresult = ref([]);
const singersonglist = useSingerSongList();
const route = useRoute();

console.log(route.hash);

if (singersonglist.value) {
  showresult.value = [...singersonglist.value];
} else {
  navigateTo("/");
}

function choosesinger(singername) {
  navigateTo("/search#" + singername);
}

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
      document.documentElement.scrollTop = 0;
    }, 100);
  }
}
onMounted(() => {
  initpage();
});
</script>

<style scoped></style>
