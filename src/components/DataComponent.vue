<template>
  <div>
    <div v-if="error">{{ error }}</div>
    <div v-else-if="data">
      <p>Base: {{ data.nowonair_list }}</p>
      <p>番組: {{ data.nowonair_list.g1 }}</p>
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import axios from 'axios';

// 状態管理のためのrefを定義
const data = ref(null);
const error = ref(null);

// APIのURL
const url = 'https://api.nhk.or.jp/v2/pg/now/130/g1.json';

// コンポーネントがマウントされた時にデータを取得
onMounted(async () => {
  try {
    // 環境変数からAPIキーを取得
    const key = import.meta.env.VITE_API_KEY;
    // パラメータとしてAPIキーを渡す
    const response = await axios.get(url, { params: { key } });
    data.value = response.data;
  } catch (err) {
    error.value = 'Error loading data: ' + err;
  }
});
</script>
