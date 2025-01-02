<script setup lang="ts">
import { ref, computed } from "vue";
interface Props {
  id: number;
  name: string;
  email: string;
  points: number;
  note?: string;
}

// const props = defineProps<Props>();
//↓computedを使わずデフォルト値を設定
const props = withDefaults(
  defineProps<Props>(),
  { note: "--" }
);

// このコンポーネント内で利用するポイント
const localPoints = ref(props.points);

// Propsのnoteを加工する算出プロパティ
// const localNote = computed(
//   (): string => {
//     let localNote = props.note;
//     if (localNote == undefined) {
//       localNote = "--";
//     }
//     return localNote;
//   }
// )

//ポイント加算ボタンをクリックしたときのメソッド
const pointUp = (): void => {
  localPoints.value++;
}
</script>

<template>
  <section class="box">
    <h4>{{ name }}さんの情報</h4>
    <dl>
      <dt>ID</dt>
      <dd>{{ id }}</dd>
      <dt>メールアドレス</dt>
      <dd>{{ email }}</dd>
      <dt>保有ポイント</dt>
      <dd>{{ localPoints }}</dd>
      <dt>備考</dt>
      <!-- <dd>{{ localNote }}</dd> -->
       <dd>{{ note }}</dd>
    </dl>

    <button v-on:click="pointUp">ポイント加算</button>
  </section>
</template>

<style scoped>
.box {
  border: 1px solid red;
  margin: 10px;
}
</style>
