<script setup lang="ts">
interface Props {
  rand: number;
}
defineProps<Props>();

interface Emits {
  (event: "createNewRand"): void;
}
const emit = defineEmits<Emits>();

const onNewRandButtonClick = (): void => {
  emit('createNewRand');
}
</script>

<template>
  <section>
    <p>子コンポーネントで乱数を表示：{{ rand }}</p>
    <button v-on:click="onNewRandButtonClick">新たな乱数を発生</button>
  </section>
</template>
