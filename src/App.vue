<template>
  <div id="app">
    <Header/>
    <Main/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "./src/assets/scss/partials/_commons.scss";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: white;
  height: 100vh;
}

body {
  background-color: $dark-blue;
}
</style>
