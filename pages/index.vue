<template>
  <div class="container">
    <ul>
      <li><nuxt-link to="gnb" class="button--green">Gnb</nuxt-link></li>
      <li><nuxt-link to="tab" class="button--green">Tab</nuxt-link></li>
    </ul>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

ul {
  padding-left: 0;
}
li {
  list-style: none;
  margin-bottom: 15px;
}
.button--green {
  width: 100%;
  margin-left: 0;
}
</style>
