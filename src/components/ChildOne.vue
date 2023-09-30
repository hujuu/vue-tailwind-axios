<template>
  <button @click="sendData">Send Data</button>
</template>

<script setup lang="ts">
import { defineEmits } from 'vue';

const emit = defineEmits();

const sendData = () => {
  emit('sendData', 'Data from ChildOne');
};
</script>
