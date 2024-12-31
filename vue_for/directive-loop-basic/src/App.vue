<script setup lang="ts">
import { ref } from "vue";

// 基本のループ
const cocktailListInit: string[] = ["ホワイトレディ", "ブルーハワイ", "ニューヨーク"];
const cocktailList = ref(cocktailListInit);

// 連想配列のループ
const cocktailListInit02: { [key: number]: string } = {
  2345: "ホワイトレディ",
  4412: "ブルーハワイ",
  6792: "ニューヨーク"
};
const cocktailList02 = ref(cocktailListInit02);
</script>
<template>
  <h1>v-for</h1>
  <section>
    <h2>基本のループ</h2>
    <ul>
      <p>リスト①</p>
      <li v-for="cocktailName in cocktailList" v-bind:key="cocktailName">
        {{ cocktailName }}
      </li>
    </ul>
    <ul>
      <p>リスト②</p>
      <li v-for="(cocktailName, index) in cocktailList" v-bind:key="cocktailName">{{ cocktailName }}(インデックス{{ index }})   </li>
    </ul>
  </section>

  <section>
    <h2>連想配列のループ</h2>
    <ul>
      <li
        v-for="(cocktailName02, id) in cocktailList02"
        v-bind:key="'cocktailList' + id">
        IDが{{ id }}のカクテルは{{ cocktailName02 }}
      </li>
    </ul>

    <ul>
      <p>インデックスも使う</p>
      <li
        v-for="(cocktailName02, id, index) in cocktailList02"
        v-bind:key="'cocktailListWithIdx' + id">
      {{ index + 1 }}: IDが{{ id }}のカクテルは{{ cocktailName02 }}
      </li>
    </ul>
  </section>
</template>

<style scoped>

</style>
