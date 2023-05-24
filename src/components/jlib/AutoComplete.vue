<script setup>
import {ref} from "vue";
let data = ref();
let showItems = ref(false)
data.value = [
  {key: 1, title: 'spain' },
  {key: 2, title: 'england' },
  {key: 3, title: 'france' },
  {key: 4, title: 'germany' },
]
let searchText = ref("")
let filteredData = ref();

const handleSelection = (selectedItem) => {
  searchText.value = selectedItem.title;
  showItems.value = false;
}
const search = () => {
  filteredData.value = data.value.filter(item => item.title.includes(searchText.value));
  showItems.value = !stringIsEmpty(searchText.value);
}
const stringIsEmpty = (str) => {
  return str === "";
}
</script>

<template>
  <div class="relative">
    <input class="border-blue-950" type="text" v-model="searchText" @keyup="search">
    <div v-show="showItems" class="bg-gray-200 p-4 absolute ">
      <div
          v-for="d in filteredData"
          @click="handleSelection(d)"
          class="px-2 cursor-pointer hover:bg-gray-100 rounded"
      >{{ d.title }}</div>
    </div>
  </div>
  <div>other text</div>
  <div>{{searchText.title}}</div>
</template>

<style scoped>

</style>