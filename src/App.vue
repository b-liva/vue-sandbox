<script setup>
import {ref} from 'vue';
import AutoComplete from "./components/jlib/AutoComplete.vue";
let selectedIem = ref();
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
  <div class="w-48">
    <AutoComplete :items-list="countries" @item="setItem"></AutoComplete>
    <div>other texts</div>
    <div>{{selectedIem}}</div>
  </div>
</template>

<style scoped>

</style>
