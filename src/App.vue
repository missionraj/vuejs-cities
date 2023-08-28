<script setup lang="ts">
import { ref, computed } from 'vue';
import City from './assets/city.json';

export interface cityInterface {
  name: string;
  count: number;
  'content:': string;
}

const cities = computed(() => {
  return City.sort(function (a: cityInterface, b: cityInterface) {
    var textA = a.name.toUpperCase();
    var textB = b.name.toUpperCase();
    return textA < textB ? -1 : textA > textB ? 1 : 0;
  });
});

const selectCity = (index: number) => {
  selectedCity.value = index;
};
const selectedCity = ref(-1);
</script>

<template>
  <div class="cities">
    <div v-for="(city, i) in cities">
      <p @click="selectCity(i)">{{ city.name }} ({{ city.count }})</p>
      <div v-if="selectedCity === i" class="details">
        <p>NAME:- {{ city.name }}</p>
        <p>COUNT:- {{ city.count }}</p>
        <p>CONTENT:- {{ city['content:'] }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cities {
  display: grid;
  grid-template-columns: 33% 33% 33%;
}
.details {
  border: 2px solid black;
  padding: 1rem;
}
</style>
