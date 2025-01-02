<script setup lang="ts">
import { ref } from "vue";
import OneSection from './components/OneSection.vue'
import OneInfo from "./components/OneInfo.vue";

const rand = Math.floor(Math.random() * 100);
const propsContent = ref(rand);
</script>

<template>
  <div>
    <h2>コンポーネントの独立性</h2>
    <OneSection />
    <OneSection />
  </div>

  <div>
    <h2>親から子へのコンポーネント間通信</h2>
    <p>Propsの基礎</p>
    <OneInfo
      title="propsの利用"
      content="子コンポーネントにデータを渡すにはPropsを利用する。"
      v-bind:props-content="propsContent"/>
  </div>
</template>

<style scoped>
</style>
