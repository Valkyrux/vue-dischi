<template>
    <select name="genreSelect" id="#genre-select"
    @change='$emit("userSelection", value)' v-model="value">
        <option value="All">All</option>
        <option
            v-for="(option,index) in optionsForSelect"
            :value="option"
            :key="index">
                {{option}}
        </option>
    </select>
</template>

<script>
export default {
  name: 'Select',
  data() {
    return {
      value: 'All',
    };
  },
  props: {
    optionsForSelect: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>

</style>
