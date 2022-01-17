<template>
  <header>
      <img src="../assets/logo-spotify-icon-4096.png" alt="spotify logo">
  </header>
</template>

<script>
export default {
    name: "Header"
}
</script>

<style lang="scss" scoped>
@import "../assets/partials/_commons.scss";
header {
    height: 100px;
    background-color: $gray;
}

img {
    width: 50px;
    text-align: start;
}
</style>
