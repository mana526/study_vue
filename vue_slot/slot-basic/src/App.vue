<script setup lang="ts">
import { ref } from "vue";
import OneSection from "./components/OneSection.vue";
import ScopeSlot from "./components/ScopeSlot.vue";

const taro = ref('田中太郎');
const jiro = ref('鈴木次郎');
const taroProblemInit = ["電話が通じません", "留守です"];
const tarpProblemList = ref(taroProblemInit);
</script>

<template>
  <!-- slotの基本 -->
  <section>
    <h1>Slotの利用</h1>
    <OneSection v-bind:name="taro">
      <!-- <p>{{ taro }}さんは連絡がつきません</p> -->
      <template v-slot:default>
        <p>問題発生</p>
      </template>
      <template v-slot:detail>
        <ul>
          <li v-for="problem in tarpProblemList">
            {{ problem }}
          </li>
        </ul>
      </template>
    </OneSection>
    <OneSection v-bind:name="jiro" />
  </section>

  <!-- スコープ付きスロット -->
  <section>
    <h1>スコープ付きslot</h1>
    <ScopeSlot>
      <template v-slot:default="slotProps">
        <dl>
          <dt>名前</dt>
          <dd>{{ slotProps.memberInfo.name }}</dd>
          <dt>状況</dt>
          <dd>{{ slotProps.memberInfo.state }}</dd>
        </dl>
      </template>
    </ScopeSlot>
  </section>
</template>

<style scoped>
</style>
