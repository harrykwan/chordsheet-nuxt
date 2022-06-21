<template>
  <div
    :class="{ 'theme-light': theme == 'light', 'theme-dark': theme == 'dark' }"
    data-gradient="body-default"
  >
    <div
      :class="{
        'fixedbg-light': theme == 'light',
        'fixedbg-dark': theme == 'dark',
      }"
    ></div>
    <Meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <Meta name="apple-mobile-web-app-capable" content="yes" />
    <Meta
      name="apple-mobile-web-app-status-bar-style"
      content="black-translucent"
    />
    <Meta
      name="viewport"
      content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, viewport-fit=cover, user-scalable=no"
    />
    <Title>BUSKKING</Title>
    <Link rel="stylesheet" type="text/css" href="styles/bootstrap.css" />
    <Link rel="stylesheet" type="text/css" href="styles/style.css" />
    <Link
      href="https://fonts.googleapis.com/css?family=Roboto:300,300i,400,400i,500,500i,700,700i,900,900i|Source+Sans+Pro:300,300i,400,400i,600,600i,700,700i,900,900i&display=swap"
      rel="stylesheet"
    />
    <Link
      rel="stylesheet"
      type="text/css"
      href="fonts/css/fontawesome-all.min.css"
    />

    <div id="preloader" v-if="loading">
      <div class="spinner-border color-highlight" role="status"></div>
    </div>
    <client-only>
      <NuxtPage />
    </client-only>
    <Script type="text/javascript" src="scripts/bootstrap.min.js"></Script>
    <Script type="text/javascript" src="scripts/custom.js"></Script>
  </div>
</template>

<script setup>
const loading = useLoadingScreen();
const theme = useTheme();

function getlocalstorage() {
  let locatheme;
  if (process.client) {
    locatheme = localStorage.getItem("theme");
  }
  if (locatheme) theme.value = locatheme;
}

onMounted(() => {
  getlocalstorage();
});

watch(theme, () => {
  if (process.client) {
    localStorage.setItem("theme", theme.value);
  }
});
</script>

<style>
.fixedbg-dark {
  background: #1b1d21;
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
}

.fixedbg-light {
  background: #f0f0f0;
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
}
</style>
