<template>
    <div class="container d-flex align-items-center
    justify-content-center overflow-auto flex-column">
        <Select :optionsForSelect="genreList" v-if="genreList"/>
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
import Select from './Select.vue';

export default {
  name: 'Main',
  components: {
    Card,
    Select,
  },
  data() {
    return {
      albumList: null,
      genreList: null,
    };
  },
  methods: {
    getKeyValueList(objectList, key) {
      const keyValueList = [];
      objectList.forEach((element) => {
        if (!keyValueList.includes(element[key])) {
          keyValueList.push(element[key]);
        }
      });
      return keyValueList;
    },
    getValues(APIUrl) {
      axios.get(APIUrl)
        .then((response) => {
          this.albumList = response.data.response;
          this.genreList = this.getKeyValueList(this.albumList, 'genre');
        })
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
