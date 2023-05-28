<script setup>
import {onMounted, ref} from "vue";
const props = defineProps(['itemList', 'selectedObject']);
const emit = defineEmits(['update:selectedObject', 'item'])
let showItems = ref(false)
let filteredData = ref();
let selectedItem = ref();
let searchTxt = ref();
onMounted(() => {
  selectedItem.value = props.selectedObject;
  searchTxt.value = selectedItem.value.title;
})
const stringIsEmpty = (str) => {
  return str === "";
}
const search = () => {
  filteredData.value = props.itemList.filter(item => item.title.includes(searchTxt.value));
  showItems.value = !stringIsEmpty(props.selectedObject.title);
}

const handleSelection = (item) => {
  selectedItem.value = item;
  searchTxt.value = selectedItem.value.title;
  showItems.value = false;
  emit('item', selectedItem.value);
}
</script>

<template>
  <div class="relative">
    <div class="grid grid-cols-5">
      <div>
        <p class="capitalize">selected item</p>
        <pre><code>{{ selectedItem }}</code></pre>
      </div>
      <div>
        <p class="capitalize">selectedObject</p>
        <pre><code>{{ selectedObject }}</code></pre>
      </div>
      <div class="">
        <p class="capitalize">item list:</p>
        <pre><code>{{ itemList }}</code></pre>
      </div>
      <div class="">
        <p class="capitalize">filtered data:</p>
        <pre><code>{{ filteredData }}</code></pre>
      </div>
      <div>
        <input
            class="border border-gray-200 focus:border-gray-400 shadow-md rounded p-1 w-full"
            type="text"
            :value="searchTxt"
            @input="searchTxt = $event.target.value"
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
    </div>
  </div>
</template>

<style scoped>

</style>