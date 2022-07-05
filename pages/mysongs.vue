<template>
  <div>
    <FooterNav />

    <div id="page" style="height: 100vh">
      <div class="page-content header-clear-small">
        <div class="search-page">
          <div
            class="search-results card card-style shadow-l"
            v-if="savedsongs || smallloading"
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
            <div v-if="savedsongs">
              <div class="content">
                <div v-if="savedsongs.length > 0">
                  已存 {{ savedsongs.length }} 首歌
                </div>

                <div
                  class="search-result-list"
                  v-for="(item, ind) in savedsongs"
                  :key="ind"
                >
                  <img
                    class="shadow-l preload-img"
                    :src="'/images/earphone.jpg'"
                  />
                  <h1 class="mt-3 songtitle">
                    {{ item.song_name }}
                    <span class="text-muted">{{ item.artist_name }}</span>
                  </h1>
                  <p>
                    {{ formatDate(item.updatetime) }}
                  </p>
                  <a
                    href="#"
                    @click="choosechord(item.chordsheet, item.id)"
                    class="bg-highlight"
                    >VIEW</a
                  >
                </div>

                <div
                  class="search-no-results"
                  v-if="savedsongs.length == 0 && !smallloading"
                >
                  <h3 class="bold top-10">暫時沒有歌單</h3>
                  <span class="under-heading font-11 opacity-70 color-theme"
                    >請在揾譜頁面加入歌曲</span
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
const loading = useLoadingScreen();
const chordsheet = useChordSheet();
const chordsheetid = useChordSheetId();
const smallloading = ref(false);
const savedsongs = ref([]);
if (process.client) {
  try {
    chordsheetid.value = "";
    savedsongs.value = [];
    const songlist = JSON.parse(localStorage.getItem("chordsheetlist"));
    songlist.map((x) => {
      const tempsheetitem = JSON.parse(localStorage.getItem(x));
      savedsongs.value.push({
        id: x,
        song_name: tempsheetitem.chordsheet.song_name,
        artist_name: tempsheetitem.chordsheet.artist_name,
        updatetime: tempsheetitem.updatetime,
        chordsheet: tempsheetitem.chordsheet,
      });
    });
  } catch (e) {}
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
    }, 100);
  }
}

onMounted(() => {
  initpage();
});

function formatDate(datetime) {
  var d = new Date(datetime),
    month = "" + (d.getMonth() + 1),
    day = "" + d.getDate(),
    year = d.getFullYear();

  if (month.length < 2) month = "0" + month;
  if (day.length < 2) day = "0" + day;

  return [year, month, day].join("-");
}

async function choosechord(item, id) {
  console.log(item);
  chordsheet.value = item;
  chordsheetid.value = id;
  loading.value = true;
  if (process.client) {
    setTimeout(() => {
      navigateTo("/chord");
    }, 200);
  }
}
</script>
