<script setup>
import {ref} from 'vue';
import AutoComplete from "./components/jlib/AutoComplete.vue";
let selectedIem = ref();
let searchText = ref('a')
let countries =ref([
      {key: 1, title: 'spain' },
      {key: 2, title: 'england' },
      {key: 3, title: 'france' },
      {key: 4, title: 'germany' },
    ]);
const setItem = (e) => {
  console.log('item fired.', e);
  selectedIem.value = e;
}
</script>

<template>
  <div class="w-64">
    <AutoComplete :search-text="searchText" @update:search-text="nv => searchText = nv" :item-list="countries" @item="setItem"></AutoComplete>
    <div><span>selected item in parent:</span> <span class="text-blue-900 font-bold">{{selectedIem?.title}}</span></div>
    <div>{{selectedIem}}</div>
  </div>
</template>

<style scoped>

</style>
