<template>
  <div class="text-amber-50">{{ data }}</div>
</template>

<script setup lang="ts">
defineProps({
  data: {
    type: String as () => string | null,
  }
});
</script>
