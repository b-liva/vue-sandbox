<script setup>
import {ref} from 'vue';
import AutoComplete from "./components/jlib/AutoComplete.vue";
let countries =ref([
      {key: 1, title: 'spain' },
      {key: 2, title: 'england' },
      {key: 3, title: 'france' },
      {key: 4, title: 'germany' },
    ]);
</script>

<template>
  <div class="w-48">
    <AutoComplete :items-list="countries"></AutoComplete>
  </div>
</template>

<style scoped>

</style>
