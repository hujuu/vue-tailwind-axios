<template>
  <div class="text-amber-50">{{ data }}</div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';

const props = defineProps({
  data: String
});
</script>
