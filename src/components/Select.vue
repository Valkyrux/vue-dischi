<template>
    <select name="genreSelect" id="#genre-select">
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
