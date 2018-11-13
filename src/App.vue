<template>
  <div id="app"><HeaderCmp /></div>
</template>

<script>
import HeaderCmp from "./components/Header.vue";

export default {
  name: "app",
  components: {
    HeaderCmp
  }
};
</script>

<style lang="stylus">
@import url('~@/assets/reset.css');

*, *::after, *::before {
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
}

body {
  font-size: 1.6rem;
  font-family: lato, sans-serif;
  color: #1a1a1a;
  background-color: #fff;
}

a {
  color: #db6356;
  text-decoration: none;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: teal;
  min-height: 100vh;
}
</style>
