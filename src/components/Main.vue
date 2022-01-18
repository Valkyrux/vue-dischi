<template>
    <div class="container overflow-auto">
      <div class="text-end w-100 p-4">
        <Select :optionsForSelect="genreList" v-if="genreList"
        @userSelection="choosedGenre = $event"
        class="me-2"/>
        <Select :optionsForSelect="artistList" v-if="artistList"
        @userSelection="choosedArtist = $event" />
      </div>
      <ul class="row row-cols-5 p-0 w-100">
        <Card
          v-for="(album, index)
          in doubleFilteredList"
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
    // funzione che raccoglie tutti i possibili valori di una chiave in una lista di oggetti unici
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
          this.artistList = this.getKeyValueList(this.albumList, 'author');
        })
        .catch((error) => { console.log(error); });
    },
    // funzione che applica un filtro dato un array di oggetti nome chiave e valore
    filterForKey(objectList, key, keyValue) {
      if (keyValue !== 'All') {
        return objectList.filter((element) => element[key] === keyValue);
      }
      return objectList;
    },
  },
  // genero una lista con doppio filtro per mostrare i risultati
  computed: {
    doubleFilteredList() {
      const firstFilter = this.filterForKey(this.albumList, 'genre', this.choosedGenre);
      return this.filterForKey(firstFilter, 'author', this.choosedArtist);
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
