<template>
  <div>
    <FooterNav />

    <div id="page">
      <div class="page-content header-clear-small">
        <div class="search-page">
          <div class="search-box search-header bg-theme card-style me-3 ms-3">
            <i class="fa fa-search"></i>
            <input
              type="text"
              class="border-0"
              placeholder="揾緊咩歌？"
              v-model="searchinput"
              v-on:change="searchchord"
            />
            <a href="#" class="clear-search disabled mt-0"
              ><i class="fa fa-times color-red-dark"></i
            ></a>
          </div>

          <div
            class="search-results card card-style shadow-l"
            v-if="searchresult || smallloading"
          >
            <div v-if="smallloading">
              <div class="content">
                <div class="d-flex justify-content-center">
                  <div
                    class="spinner-border color-red-dark"
                    role="status"
                  ></div>
                </div>
              </div>
            </div>
            <div v-if="searchresult">
              <div class="content">
                <div v-if="searchresult.length > 0">
                  找到 {{ searchresult.length }} 個結果
                </div>

                <div
                  class="search-result-list"
                  v-for="(item, ind) in searchresult"
                  :key="ind"
                >
                  <img class="shadow-l preload-img" :src="item.image" />
                  <h1 class="mt-3">{{ item.song_name }}</h1>
                  <p>{{ item.artist_name }}</p>
                  <a href="#" @click="choosechord(item)" class="bg-highlight"
                    >VIEW</a
                  >
                </div>

                <div
                  class="search-no-results"
                  v-if="searchresult.length == 0 && !smallloading"
                >
                  <h3 class="bold top-10">暫時沒有這首歌/歌手資料</h3>
                  <span class="under-heading font-11 opacity-70 color-theme"
                    >請試試其他關鍵字眼</span
                  >
                </div>
              </div>
            </div>
          </div>

          <div class="search-trending card card-style disabled">
            <div class="content mb-2">
              <h3>人氣歌曲</h3>
              <p class="font-11 mt-n2">其他人在彈什麼？</p>
            </div>
            <div class="list-group list-custom-small me-3 ms-3">
              <a href="#">
                <span class="font-400 color-blue-dark">All Products</span>
                <i class="color-gray-dark fa fa-angle-right"></i>
              </a>
              <a href="#">
                <span class="font-400 color-blue-dark">Eazy Mobile</span>
                <i class="color-gray-dark fa fa-angle-right"></i>
              </a>
              <a href="#">
                <span class="font-400 color-blue-dark">Mega Mobile</span>
                <i class="color-gray-dark fa fa-angle-right"></i>
              </a>
              <a href="#">
                <span class="font-400 color-blue-dark">Ultra Mobile</span>
                <i class="color-gray-dark fa fa-angle-right"></i>
              </a>
              <a href="#">
                <span class="font-400 color-blue-dark">Kolor Mobile</span>
                <i class="color-gray-dark fa fa-angle-right"></i>
              </a>
              <a href="#" class="border-0">
                <span class="font-400 color-blue-dark">Vinga Mobile</span>
                <i class="color-gray-dark fa fa-angle-right"></i>
              </a>
            </div>
          </div>

          <div
            class="card card-style preload-img"
            data-src="images/pictures/18.jpg"
            data-card-height="130"
          >
            <div class="card-center ms-3">
              <h1 class="color-white mb-0">隨機</h1>
              <p class="color-white mt-n1 mb-0">是但唱一首</p>
            </div>
            <div class="card-center me-3">
              <a
                href="#"
                data-back-button
                class="btn btn-m float-end rounded-xl shadow-xl text-uppercase font-800 bg-highlight"
                >GO</a
              >
            </div>
            <div class="card-overlay bg-black opacity-80"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const searchinput = ref("");
const searchresult = useSearchResult();
const chordsheet = useChordSheet();
const loading = useLoadingScreen();
const smallloading = ref(false);
loading.value = true;

async function searchchord() {
  smallloading.value = true;
  searchresult.value = [];
  let guitarian_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/search/guitarian/" +
      encodeURIComponent(searchinput.value)
  );
  guitarian_result = guitarian_result.data.value.body;
  guitarian_result = guitarian_result.map((x) => {
    return {
      ...x,
      image: "images/guitarian.png",
    };
  });
  searchresult.value = guitarian_result;

  let polygon_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/search/polygon/" +
      encodeURIComponent(searchinput.value)
  );

  polygon_result = polygon_result.data.value.body;
  polygon_result = polygon_result.map((x) => {
    return {
      ...x,
      image: "images/polygon.jpg",
    };
  });
  console.log(polygon_result);
  searchresult.value = [...polygon_result, ...searchresult.value];
  smallloading.value = false;
}

async function choosechord(item) {
  loading.value = true;
  let chord_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/getchord?url=" +
      encodeURI(item.url)
  );
  chord_result = chord_result.data.value.body;
  chordsheet.value = {
    ...item,
    chordsheet: chord_result,
    transpose: 0,
  };
  navigateTo("/chord");
}

onMounted(() => {
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
