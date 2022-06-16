<template>
  <div>
    <FooterNav />
  </div>
</template>

<script setup>
const loading = useLoadingScreen();
loading.value = true;
onMounted(() => {
  if (process.client) {
    try {
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
