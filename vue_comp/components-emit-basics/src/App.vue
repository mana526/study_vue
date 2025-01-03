<script setup lang="ts">
import { ref, computed } from "vue";
import OneSection from "./components/OneSection.vue";
import OneMember from "./components/OneMember.vue";

// 乱数用
const randInit = Math.round(Math.random() * 10);
const rand = ref(randInit);

const onCreateNewRand = () => {
  rand.value = Math.round(Math.random() * 10);
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

// emitによって実行されるメソッド
const onIncrementPoint = (id: number): void => {
  const member = memberList.value.get(id);
  if (member != undefined) {
    member.points++;
  }
}

interface Member {
  id: number;
  name: string;
  email: string;
  points: number;
  note?: string;
}
</script>

<template>
  <section>
    <h2>親コンポーネントの乱数:{{ rand }}</h2>
    <OneSection
      v-on:click="onCreateNewRand"
      v-bind:rand="rand"/>
  </section>

  <h1>propsの応用</h1>
  <section>
    <h2>会員リスト</h2>
    <p>全会員の保有ポイントの合計：{{ totalPoints }}</p>
    <OneMember v-for="[id, member] of memberList" v-bind:key="id" v-bind:id="id" v-bind:name="member.name" v-bind:email="member.email" v-bind:points="member.points" v-bind:note="member.note"
    v-on:increment="onIncrementPoint"/>
  </section>
</template>

<style scoped></style>
