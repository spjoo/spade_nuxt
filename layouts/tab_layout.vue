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
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@100;300;400;500;700;900&display=swap");

html {
  font-family: "Noto Sans KR", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

a {
  text-decoration: none;
  color: inherit;
}

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
  justify-content: center;
  text-align: center;
}
</style>
