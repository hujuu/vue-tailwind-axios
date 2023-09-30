<template>
  <div>
    <div v-if="error">{{ error }}</div>
    <div v-else-if="data">
      <p>Base: {{ data.nowonair_list }}</p>
      <p>番組: {{ data.nowonair_list.g1 }}</p>
      <div class="text-amber-50">{{ service }}</div>
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script setup lang="ts">
import { ref, watchEffect } from 'vue';
import axios from 'axios';

const props = defineProps({
  service: {
    type: String as () => string | null,
  }
});

const data = ref(null);
const error = ref(null);

watchEffect(async () => {
  if (!props.service) return;

  const url = `https://api.nhk.or.jp/v2/pg/now/130/${props.service}.json`;
  try {
    const key = import.meta.env.VITE_API_KEY;
    const response = await axios.get(url, { params: { key } });
    data.value = response.data;
  } catch (err) {
    error.value = 'Error loading data: ' + err + ' ' + url;
  }
});
</script>
