<script setup>
import {ref} from 'vue';
import AutoComplete from "./components/jlib/AutoComplete.vue";
let objs = ref([{key: 1, title:'spain'}])
let countries =ref([
      {key: 1, title: 'spain' },
      {key: 2, title: 'england' },
      {key: 3, title: 'france' },
      {key: 4, title: 'germany' },
    ]);
const setItem = (obj, e) => {
  Object.assign(obj, countries.value.filter(item => item.key === e.key)[0])
}
</script>

<template>
  <div>
    <div>
      <p>objs: </p>
      <pre><code>{{objs}}</code></pre>
    </div>
    <AutoComplete
        v-for="obj in objs"
        :selected-object="obj"
        :item-list="countries"
        @item="setItem(obj, $event)">
    </AutoComplete>
  </div>
</template>

<style scoped>

</style>
