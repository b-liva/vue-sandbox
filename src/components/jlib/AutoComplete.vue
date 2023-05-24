<script setup>
import {ref} from "vue";
const props = defineProps(['itemsList'])

let showItems = ref(false)
let searchText = ref("")
let filteredData = ref();

const handleSelection = (selectedItem) => {
  searchText.value = selectedItem.title;
  showItems.value = false;
}
const search = () => {
  filteredData.value = props.itemsList.filter(item => item.title.includes(searchText.value));
  showItems.value = !stringIsEmpty(searchText.value);
}
const stringIsEmpty = (str) => {
  return str === "";
}
</script>

<template>
  <div class="relative">
    <input class="border border-gray-200 focus:border-gray-400 shadow-md rounded p-1 w-full" type="text" v-model="searchText" @keyup="search">
    <div v-show="showItems" class="bg-white border-blue-950 shadow-md absolute w-full rounded" @focusout="showItems=false">
      <div
          v-for="d in filteredData"
          @click="handleSelection(d)"
          class="cursor-pointer hover:bg-gray-100 rounded pb-0.5 my-1 mx-1 pl-2"
      >{{ d.title }}</div>
    </div>
  </div>
  <div>other text</div>
  <div>{{searchText.title}}</div>
</template>

<style scoped>

</style>