<script setup>
import {ref} from 'vue';
import AutoComplete from "./components/misc/AutoComplete.vue";
let countries =ref([
      {key: 1, title: 'spain' },
      {key: 2, title: 'england' },
      {key: 3, title: 'france' },
      {key: 4, title: 'germany' },
    ]);
let fruits = [ 'Apple', 'Banana', 'Orange', 'Mango', 'Pear', 'Peach', 'Grape', 'Tangerine', 'Pineapple'];
</script>

<template>
  <div class="w-48">
    <AutoComplete :items="fruits"></AutoComplete>
  </div>
</template>

<style scoped>

</style>
