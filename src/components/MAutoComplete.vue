<script setup>
import AutoComplete from 'primevue/autocomplete';
import { ref } from "vue";

const countries = ref([
  {key: 1, name: 'spain'},
  {key: 2, name: 'germany'},
  {key: 3, name: 'france'},
  {key: 4, name: 'england'},
  {key: 5, name: 'england2'},
  {key: 6, name: 'newengland'},
]);
const selectedCountry = ref();
const filteredCountries = ref();

const search = (event) => {
  setTimeout(() => {
    if (!event.query.trim().length) {
      filteredCountries.value = [...countries.value];
    } else {
      filteredCountries.value = countries.value.filter((country) => {
        return country.name.toLowerCase().includes(event.query.toLowerCase());
      });
    }
  }, 250);
}
</script>

<template>
  <p>cou:{{selectedCountry}}</p>
  <div>
    <AutoComplete v-model="selectedCountry" optionLabel="name" :suggestions="filteredCountries" @complete="search" />
  </div>
</template>

<style scoped>

</style>