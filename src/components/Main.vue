<template>
    <div class="container d-flex align-items-center
    justify-content-center overflow-auto flex-column"
    >
        <Select :optionsForSelect="genreList" v-if="genreList"
        @userSelection="choosedGenre = $event" />
        <Select :optionsForSelect="artistList" v-if="artistList"
        @userSelection="choosedArtist = $event" />
        <ul class="row row-cols-5 p-0">
            <Card
            v-for="(album, index)
            in doubleFilter(albumList, 'genre', 'author', choosedGenre, choosedArtist)"
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
      artistList: null,
      choosedGenre: 'All',
      choosedArtist: 'All',
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
    filterForKey(objectList, key, keyValue) {
      if (keyValue !== 'All') {
        return objectList.filter((element) => element[key] === keyValue);
      }
      return objectList;
    },
    doubleFilter(objectList, keyOne, keyTwo, keyValueOne, keyValueTwo) {
      const firstFilter = this.filterForKey(objectList, keyOne, keyValueOne);
      return this.filterForKey(firstFilter, keyTwo, keyValueTwo);
    },
    getValues(APIUrl) {
      axios.get(APIUrl)
        .then((response) => {
          this.albumList = response.data.response;
          this.genreList = this.getKeyValueList(this.albumList, 'genre');
          this.artistList = this.getKeyValueList(this.albumList, 'author');
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
