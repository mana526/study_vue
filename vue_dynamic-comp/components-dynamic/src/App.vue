<script setup lang="ts">
import { shallowRef } from "vue";
import Input from "./components/Input.vue";
import Radio from "./components/Radio.vue";
import Select from "./components/Select.vue";

// shallowRefとはリアクティブにする範囲を浅くする場合に使用。パフォーマンスが向上する。refはすべての値を常に監視している。
const currentComp = shallowRef(Input);
const currentCompName = shallowRef("input");

const compList = [Input, Radio, Select];
const compNameList: string[] = ["input", "radio", "select"];

let currentCompIndex = 0;

const switchComp = (): void => {
  console.log(currentCompIndex);
  currentCompIndex++;
  if (currentCompIndex >= 3) {
    currentCompIndex = 0;
  }
  currentComp.value = compList[currentCompIndex];
  currentCompName.value = compNameList[currentCompIndex];
}

</script>

<template>
  <p>コンポーネント名：{{ currentCompName }}</p>
  <KeepAlive>
    <component v-bind:is="currentComp"/>
  </KeepAlive>

  <button v-on:click="switchComp">切り替え</button>
</template>

<style scoped></style>
