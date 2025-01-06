<script setup lang="ts">
import { ref, computed } from "vue";
import OneMember from "./components/OneMember.vue";
import ResetButton from "./components/ResetButton.vue";

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
// const onIncrementPoint = (id: number): void => {
//   const member = memberList.value.get(id);
//   if (member != undefined) {
//     member.points++;
//   }
// }

interface Member {
  id: number;
  name: string;
  email: string;
  points: number;
  note?: string;
}

//emit復習
const count = ref(0);

const countUp = () => {
  count.value++;
}

const countReset = () => {
  count.value = 0;
}

const onReset = (value) => {
  count.value = value;
}
</script>

<template>
  <section>
    <h2>会員リスト</h2>
    <p>全会員の保有ポイントの合計：{{ totalPoints }}</p>
    <OneMember v-for="[id, member] of memberList" v-bind:key="id" v-bind:id="id" v-bind:name="member.name" v-bind:email="member.email" v-model:points="member.points" v-bind:note="member.note"/>
  </section>

  <section>
    <h2>emit復習</h2>
    <p>{{ count }}</p>
    <button @click="countUp">カウント</button>
    <!-- <ResetButton @reset="countReset"></ResetButton> -->
    <!-- <ResetButton @hundred="count = $event"></ResetButton> -->
     <ResetButton @onReset="onReset" />
  </section>
</template>

<style scoped></style>
