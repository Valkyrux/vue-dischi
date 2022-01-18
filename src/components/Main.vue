<template>
    <div class="container d-flex align-items-center justify-content-center overflow-auto">
        <ul class="row row-cols-5 p-0">
            <Card
            v-for="(album, index) in albumList"
            :key="index"
            :imgUrl="album.poster"
            :firstTitle="album.title"
            :secondTitle="album.author"
            :thirdTitle="album.year"
            />
        </ul>
    </div>
</template>

<script>
import axios from 'axios';
import Card from './Card.vue';

export default {
  name: 'Main',
  components: {
    Card,
  },
  data() {
    return {
      albumList: null,
    };
  },
  methods: {
    getValues(APIUrl) {
      axios.get(APIUrl)
        .then((response) => { this.albumList = response.data.response; })
        .catch((error) => { console.log(error); });
    },
  },
  created() {
    this.getValues('https://flynn.boolean.careers/exercises/api/array/music');
  },
};
</script>

<style lang="scss">
@import "../assets/scss/partials/_commons.scss";

div.container {
  height: calc(100% - $header-height);
}

ul {
    list-style-type: none;
}
</style>
