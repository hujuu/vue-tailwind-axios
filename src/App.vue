<script setup lang="ts">
import {ref, computed} from "vue";
import {divideTwoNums} from "./functions.ts";
import HelloWorld from './components/HelloWorld.vue'
import DataComponent from './components/DataComponent.vue'
import ServiceSelect from './components/ServiceSelect.vue';
import ChildOne from './components/ChildOne.vue';
import ChildTwo from './components/ChildTwo.vue';

const data = ref<string | null>(null);
const service = ref<string | null>(null);

const receiveData = (value: string) => {
  data.value = value;
};

const selectedPerson = ref<{ id: string; name: string; } | null>(null);

const handleSelected = (person: { id: string; name: string }) => {
  console.log('Selected person:', person)
  selectedPerson.value = person
  service.value = person.id
}

const num1 = ref(6);
const num2 = ref(3);
const ans = computed(
    (): number => {
      return divideTwoNums(num1.value, num2.value);
    }
);
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
  <p>{{num1}}÷{{num2}}={{ans}}</p>
  <DataComponent :service="service" />
  <ServiceSelect @update:selected="handleSelected" />
  <div v-if="selectedPerson">
    Selected Person: {{ selectedPerson.name }}
  </div>
  <ChildOne @sendData="receiveData" />
  <ChildTwo :data="data" />
</template>
