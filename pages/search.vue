<template>
  <div>
    <FooterNav />

    <div id="page" style="height: 100vh">
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
                  <h1 class="mt-3 songtitle">{{ item.song_name }}</h1>
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
                @click="gettopsongs"
                class="btn btn-m float-end rounded-xl shadow-xl text-uppercase font-800 bg-highlight"
                >GO</a
              >
            </div>
            <div class="card-overlay bg-black opacity-80"></div>
          </div>

          <div
            class="search-trending card card-style"
            v-if="showtopsongs.length > 0"
          >
            <div class="content mb-2">
              <h3>人氣歌曲</h3>
              <p class="font-11 mt-n2">其他人在聽什麼？</p>
            </div>
            <div class="list-group list-custom-small me-3 ms-3">
              <a
                @click="choosetopsong(item.song_name)"
                href="#"
                v-for="(item, ind) in showtopsongs"
                :key="ind"
              >
                <span class="font-400"
                  >《 {{ item.song_name }} 》
                  <span class="font-200" style="margin-left: 10px; opacity: 0.7"
                    >[{{ item.artist_name }}]</span
                  ></span
                >
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
const searchinput = ref("");
const topsongs = ref([]);
const showtopsongs = ref([]);
const searchresult = useSearchResult();
const chordsheet = useChordSheet();
const loading = useLoadingScreen();
const smallloading = ref(false);
loading.value = true;

async function add_google_search() {
  const google_result = await googleit(searchinput.value);
  searchresult.value = [...searchresult.value, ...google_result];
}

async function add_guitarian_search() {
  let guitarian_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/search/guitarian/" +
      encodeURIComponent(searchinput.value)
  );
  guitarian_result = guitarian_result.data.value.body;
  guitarian_result = guitarian_result.map((x) => {
    return {
      ...x,
      image:
        "https://imagedelivery.net/F-3JVW4H1_xFj9Tfzrx6uA/51f900b8-090c-42f3-5255-76d1f3b3b900/public",
    };
  });
  searchresult.value = [...searchresult.value, ...guitarian_result];
}

async function add_polygon_search() {
  let polygon_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/search/polygon/" +
      encodeURIComponent(searchinput.value)
  );

  polygon_result = polygon_result.data.value.body;
  polygon_result = polygon_result.map((x) => {
    return {
      ...x,
      image:
        "https://imagedelivery.net/F-3JVW4H1_xFj9Tfzrx6uA/3edfd08f-3eb7-491d-31ec-d581d16d8800/public",
    };
  });

  searchresult.value = [...searchresult.value, ...polygon_result];
}

async function add_nineone_search() {
  let nineone_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/search/nineone/" +
      encodeURIComponent(searchinput.value)
  );

  nineone_result = nineone_result.data.value.body;
  nineone_result = nineone_result.map((x) => {
    return {
      ...x,
      image:
        "https://imagedelivery.net/F-3JVW4H1_xFj9Tfzrx6uA/044eefcd-c4b4-4aee-bcc4-111ca35cb900/public",
    };
  });

  searchresult.value = [...searchresult.value, ...nineone_result];
}

async function add_guitarian_topsongs() {
  let guitarian_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/gettopsongs/guitarian/" +
      encodeURIComponent(searchinput.value)
  );
  guitarian_result = guitarian_result.data.value.body;
  topsongs.value.push(...guitarian_result);
}

async function add_nineone_topsongs() {
  let nineone_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/gettopsongs/nineone/" +
      encodeURIComponent(searchinput.value)
  );
  nineone_result = nineone_result.data.value.body;
  topsongs.value.push(...nineone_result);
}

async function add_applemusic_topsongs() {
  let applemusic_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/gettopsongs/applemusic/" +
      encodeURIComponent(searchinput.value)
  );
  applemusic_result = applemusic_result.data.value.body;
  topsongs.value.push(...applemusic_result);
}

async function add_spotify_topsongs() {
  let spotify_result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/gettopsongs/spotify/" +
      encodeURIComponent(searchinput.value)
  );
  spotify_result = spotify_result.data.value.body;
  topsongs.value.push(...spotify_result);
}

async function gettopsongs() {
  smallloading.value = true;
  showtopsongs.value = [];
  if (topsongs.value.length == 0) {
    await Promise.all([
      add_guitarian_topsongs(),
      add_nineone_topsongs(),
      add_applemusic_topsongs(),
      //   add_spotify_topsongs(),
    ]);
  }
  for (var j = 0; j < 10; j++) {
    const randomindex = Math.floor(Math.random() * topsongs.value.length);
    const topsong = topsongs.value.splice(randomindex, 1)[0];
    showtopsongs.value.push(topsong);
  }

  smallloading.value = false;
}

function choosetopsong(song_name) {
  searchinput.value = song_name;
  searchchord();
}

async function searchchord() {
  smallloading.value = true;
  searchresult.value = [];
  await Promise.all([
    add_google_search(),
    add_guitarian_search(),
    add_polygon_search(),
    add_nineone_search(),
  ]);
  smallloading.value = false;
}

async function googleit(keyword) {
  let result = await useFetch(
    "https://7aof7x0rkc.execute-api.us-east-1.amazonaws.com/search/googleit/" +
      encodeURIComponent(keyword)
  );

  result = result.data.value.body;
  let resultlist = [];
  result.map((x) => {
    if (
      x.link.indexOf("guitarians.com/chord/") != -1 ||
      x.link.indexOf("polygon.guitars/score/") != -1 ||
      x.link.indexOf("91pu.com.tw/song/") != -1
    )
      resultlist.push({
        song_name: x.title,
        artist_name: x.link.split("//")[1].split("/")[0],
        url: x.link,
        image:
          "https://imagedelivery.net/F-3JVW4H1_xFj9Tfzrx6uA/2034dd3f-a9ab-4753-fdf9-a1bb4fe1a100/public",
      });
  });
  return resultlist;
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
<style scoped>
.songtitle {
  width: calc(100% - 80px);
}
</style>
