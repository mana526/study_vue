<script setup lang="ts">
//明示的にしているだけで、そこまで重要でもない。これがなくてもemitは動く。
defineEmits(['onReset']);
</script>

<template>
  <!-- <button @click="$emit('reset')">リセット</button> -->
  <!-- <button @click="$emit('hundred', 100)">100にする</button> -->
   <button @click="$emit('onReset', 100)">メソッドでリセット</button>
</template>
