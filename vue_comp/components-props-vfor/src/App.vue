<script setup lang="ts">
import { ref, computed } from "vue";
import OneInfo from "./components/OneInfo.vue";
import OneMember from "./components/OneMember.vue";

const weatherListInit = new Map<number, Weather>();
weatherListInit.set(1, { id: 1, title: "今日の天気", content: "今日は一日中、晴れでしょう。" });
weatherListInit.set(2, { id: 2, title: "明日の天気", content: "明日は一日中、雨でしょう。" });
weatherListInit.set(3, { id: 3, title: "明後日の天気", content: "明後日は一日中、雪でしょう。" });
const weatherList = ref(weatherListInit);

interface Weather {
  id: number;
  title: string;
  content: string;
}

//会員リスト用
const memberListInit = new Map<number, Member>();
memberListInit.set(3345, { id: 3345, name: "田中", email: "bow@example.com", points: 35, note: "初回入会特典あり。" });
memberListInit.set(1234, { id: 1234, name: "中村", email: "mue@example.com", points: 45, });
const memberList = ref(memberListInit);

//会員リスト内の全会員のポイント合計の算出プロパティ
const totalPoints = computed(
  (): number => {
    let total = 0;
    for (const member of memberList.value.values()) {
      total += member.points;
    }
    return total;
  }
)

interface Member {
  id: number;
  name: string;
  email: string;
  points: number;
  note?: string;
}
</script>

<template>
  <h1>props基礎</h1>
  <section>
    <h2>ループでコンポーネントを生成</h2>
    <OneInfo
      v-for="[id, weather] in weatherList"
      v-bind:key="id"
      v-bind:title="weather.title"
      v-bind:content="weather.content"/>
  </section>

  <h1>propsの応用</h1>
  <section>
    <h2>会員リスト</h2>
    <p>全会員の保有ポイントの合計：{{ totalPoints }}</p>
    <OneMember
      v-for="[id, member] of memberList"
      v-bind:key="id"
      v-bind:id="id"
      v-bind:name="member.name"
      v-bind:email="member.email"
      v-bind:points="member.points"
      v-bind:note="member.note"/>
  </section>
</template>

<style scoped>
</style>
