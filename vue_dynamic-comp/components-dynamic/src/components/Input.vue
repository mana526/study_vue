<script setup lang="ts">
import { ref } from "vue";
const inputNmeModel = ref("田中太郎");
</script>
<template>
  <input type="text" v-model="inputNmeModel">
  <p>{{ inputNmeModel }}</p>
</template>
