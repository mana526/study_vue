<script setup lang="ts">
interface Props {
  name: string;
}

defineProps<Props>();
</script>
<template>
  <section>
    <h2>{{ name }}さんの状況</h2>
    <slot>
      <!-- <p>問題ありません</p> -->
       <p>{{ name }}さんは問題ありません</p>
    </slot>

    <h4>詳細内容</h4>
    <slot name="detail">
      <p>特にありません</p>
    </slot>
  </section>
</template>
