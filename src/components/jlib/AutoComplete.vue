<script setup>
import {onMounted, onUnmounted, ref, watch} from "vue";

const props = defineProps(['items', 'isAsync'])
const emit = defineEmits(['input'])
let isOpen = ref(false)
let results = ref([])
let search = ref("")
let isLoading = ref(false)
let arrowCounter = ref(0)

function onChange() {
  console.log('change')
  // Let's warn the parent that a change was made
  emit("input", search.value);

  // Is the data given by an outside ajax request?
  if (props.isAsync) {
    isLoading.value = true;
  } else {
    // Let's search our flat array
    filterResults();
    isOpen.value = true;
  }
}

function filterResults() {
  // first uncapitalize all the things
  results.value = props.items.filter(item => {
    return item.toLowerCase().indexOf(search.value.toLowerCase()) > -1;
  });
}

function setResult(result) {
  search.value = result;
  isOpen.value = false;
}

function onArrowUp() {
  if (arrowCounter.value > 0) {
    arrowCounter.value = arrowCounter.value - 1;
  }
}

function onArrowDown() {
  if (arrowCounter.value < results.value.length) {
    arrowCounter.value = arrowCounter.value + 1;
  }
}

function onEnter() {
  search.value = results.value[arrowCounter.value];
  isOpen.value = false;
  arrowCounter.value = -1;
}

function handleClickOutside(evt) {
  if (!this.$el.contains(evt.target)) {
    isOpen.value = false;
    arrowCounter.value = -1;
  }
}
watch(
    () => props.items,
    (val, oldValue) => {
      // actually compare them
      if (val.length !== oldValue.length) {
        results.value = val;
        isLoading.value = false;
      }
    }
)

onMounted(() => document.addEventListener("click", handleClickOutside));
onUnmounted(() => document.removeEventListener("click", handleClickOutside));
</script>

<template>
  <div class="autocomplete">
    <input type="text" @input="onChange" v-model="search" @keyup.down="onArrowDown" @keyup.up="onArrowUp"
           @keyup.enter="onEnter"/>
    <ul id="autocomplete-results" v-show="isOpen" class="autocomplete-results">
      <li class="loading" v-if="isLoading">
        Loading results...
      </li>
      <li v-else v-for="(result, i) in results" :key="i" @click="setResult(result)" class="autocomplete-result"
          :class="{ 'is-active': i === arrowCounter }">
        {{ result }}
      </li>
    </ul>

  </div>
</template>

<style scoped>

</style>