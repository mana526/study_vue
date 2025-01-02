 <script setup lang="ts">
interface Props {
  title: string;
  content: string;
  propsContent: number;
}

defineProps<Props>();
</script>

<template>
  <section>
    <h4>{{ title }}</h4>
    <p>{{ content }}</p>
    <p>{{ propsContent }}</p>
  </section>
</template>
