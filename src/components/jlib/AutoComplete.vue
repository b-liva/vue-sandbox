<script setup>
import {ref} from "vue";
const props = defineProps(['itemsList']);
const emit = defineEmits(['item'])

let showItems = ref(false)
let searchText = ref("")
let filteredData = ref();
let selectedItem = ref();

const stringIsEmpty = (str) => {
  return str === "";
}

const search = () => {
  filteredData.value = props.itemsList.filter(item => item.title.includes(searchText.value));
  showItems.value = !stringIsEmpty(searchText.value);
}

const handleSelection = (item) => {
  searchText.value = item.title;
  selectedItem.value = item;
  showItems.value = false;
  emit('item', selectedItem.value)
}
</script>

<template>
  <div class="relative">
    <input
        class="border border-gray-200 focus:border-gray-400 shadow-md rounded p-1 w-full"
        type="text"
        v-model="searchText"
        @keyup="search">
    <div v-show="showItems" class="z-20 bg-white border-blue-950 shadow-md absolute w-full rounded" @focusout="showItems=false">
      <div
          v-for="d in filteredData"
          :key="d.key"
          @click="handleSelection(d)"
          class="cursor-pointer hover:bg-gray-100 rounded pb-0.5 my-1 mx-1 pl-2"
      >{{ d.title }}</div>
    </div>
  </div>
</template>

<style scoped>

</style>