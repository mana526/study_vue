<script setup lang="ts">
import { ref, computed } from "vue";

const radiusInit = Math.floor(Math.random() * 10);
const PI = ref(3.14);
const radius = ref(radiusInit);
// const areaInit = PI.value * radiusInit * radiusInit;
// const area = ref(areaInit);

const area = computed(
  (): number => {
    return radius.value * radius.value * PI.value;
  }
);
</script>

<template>
  <p>半径{{ radius }}の円の面積を円周率{{ PI }}で計算すると、{{ area }}</p>
</template>

<style scoped>
</style>
