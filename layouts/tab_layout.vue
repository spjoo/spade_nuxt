<template>
  <div id="wrapper">
    <header id="header">
      <div class="page_tit">
        <h1>나의 상담</h1>
      </div>
    </header>
    <Nuxt />
    <footer></footer>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
#header {
  display: flex;
  align-items: center;
  height: 50px;
}
.page_tit {
  width: 100%;
  text-align: center;
}
.page_tit h1 {
  font-size: 16px;
  font-weight: 400;
  color: #212121;
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  text-align: center;
  flex-direction: column;
}
</style>
