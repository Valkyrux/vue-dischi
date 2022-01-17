<template>
  <header class="d-flex align-items-center">
      <img src="../assets/logo-spotify-icon-4096.png" alt="spotify logo">
  </header>
</template>

<script>
export default {
  name: 'Header',
};
</script>

<style lang="scss" scoped>
@import "~bootstrap/scss/bootstrap";
@import "../assets/scss/partials/_commons.scss";

header {
    height: $header-height;
    background-color: $gray;
    text-align: start;
}

img {
    width: 50px;
}
</style>
