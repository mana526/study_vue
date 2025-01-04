<script setup lang="ts">
import { ref } from "vue";

const memberInfo = ref({
  name: "松田聖子",
  state: "問題ありません"
});
</script>

<template>
  <section>
    <slot v-bind:memberInfo="memberInfo">
      <h1>{{ memberInfo.name }}さんの状況</h1>
      <p>{{ memberInfo.state }}</p>
    </slot>
  </section>
</template>
