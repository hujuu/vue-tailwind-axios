<script setup lang="ts">
import { ref } from 'vue';

import HelloWorld from './components/HelloWorld.vue'
import DataComponent from './components/DataComponent.vue'
import ServiceSelect from './components/ServiceSelect.vue';
import ChildOne from './components/ChildOne.vue';
import ChildTwo from './components/ChildTwo.vue';

const data = ref<string | null>(null);

const receiveData = (value: string) => {
  data.value = value;
};


const selectedPerson = ref(null)

const handleSelected = (person) => {
  console.log('Selected person:', person)
  selectedPerson.value = person
}
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
  <DataComponent />
  <ServiceSelect @update:selected="handleSelected" />
  <div v-if="selectedPerson">
    Selected Person: {{ selectedPerson.name }}
  </div>
  <ChildOne @sendData="receiveData" />
  <ChildTwo :data="data" />
</template>
