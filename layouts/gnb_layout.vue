<template>
  <div id="wrapper">
    <Header />
    <Nuxt />
    <Footer />
  </div>
</template>

<script>
import Header from "../components/Header.vue";
export default {
  components: {
    Header
  }
};
</script>

<style scoped>
#wrapper {
  position: relative;
  padding-left: calc(281px + 30px);
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
