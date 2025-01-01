<script setup lang="ts">
import { ref, computed } from "vue";
const cocktailDataListInit: Cocktail[] = [
  { id: 2345, name: "ホワイトレディ", price: 1200 },
  { id: 4412, name: "ブルーハワイ", price: 1500 },
  { id: 6792, name: "ニューヨーク", price: 1100 }
];
const cocktailDataList = ref(cocktailDataListInit);
const cocktail1500 = computed(
  (): Cocktail[] => {
    const newList = cocktailDataList.value.filter(
      (cocktailItem: Cocktail): boolean => {
        return cocktailItem.price == 1500;
      }
    )
    return newList;
  }
)

interface Cocktail {
  id: number;
  name: string;
  price: number;
}
</script>

<template>
  <section>
    <p>すべてのカクテル</p>
    <ul>
      <li
        v-for="(cocktailData) in cocktailDataList"
        v-bind:key="cocktailData.id">
        id：{{ cocktailData.id }}のカクテルは{{ cocktailData.name }}
      </li>
    </ul>
  </section>
</template>

<style scoped>
</style>
