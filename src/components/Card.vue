<template>
    <li class="col mb-3">
        <div class="p-4 card-content h-100">
            <img :src="imgUrl" :alt="firstTitle" class="img-fluid">
            <h2 class="fs-4 mt-3">{{firstTitle}}</h2>
            <h3 class="fs-6">{{secondTitle}}</h3>
            <h4 class="fs-6">{{thirdTitle}}</h4>
        </div>
    </li>
</template>

<script>
export default {
  name: 'Card',
  props: {
    imgUrl: String,
    firstTitle: {
      type: String,
      require: true,
    },
    secondTitle: {
      type: String,
      required: true,
    },
    thirdTitle: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/partials/_commons.scss";

.card-content {
  background-color: $gray;
}

h3, h4 {
  color: gray;
}
</style>
