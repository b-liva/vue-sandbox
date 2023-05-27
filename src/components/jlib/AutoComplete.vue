<script setup>
import {ref} from "vue";
const props = defineProps(['itemList', 'searchText']);
const emit = defineEmits(['update:modelValue'])

let showItems = ref(false)
let filteredData = ref();
let selectedItem = ref();

const stringIsEmpty = (str) => {
  return str === "";
}

const search = () => {
  filteredData.value = props.itemList.filter(item => {
    console.log(item);
    return item.title.includes(props.searchText)
  });
  showItems.value = !stringIsEmpty(props.searchText.value);
}

const handleSelection = (item) => {
  selectedItem.value = item;
  showItems.value = false;
  emit('item', selectedItem.value)
}
</script>

<template>
  <div class="relative">
    <p>st: {{searchText}}</p>
    <p>it: {{itemList}}</p>
    <p>fd: {{filteredData}}</p>
    <input
        class="border border-gray-200 focus:border-gray-400 shadow-md rounded p-1 w-full"
        type="text"
        :value="searchText"
        @input="$emit('update:searchText', $event.target.value)"
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