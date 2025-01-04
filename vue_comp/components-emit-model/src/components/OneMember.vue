<script setup lang="ts">
import { ref, computed } from "vue";
interface Props {
  id: number;
  name: string;
  email: string;
  points: number;
  note?: string;
}

//emitの利用
// interface Emits {
//   (event: "increment", id: number): void;
// }

//↓v-modelを使った子から親への通信
interface Emits {
  (event: "update:points", points: number): void;
}
const emit = defineEmits<Emits>();

// const props = defineProps<Props>();
//↓computedを使わずデフォルト値を設定
const props = withDefaults(
  defineProps<Props>(),
  { note: "--" }
);

// このコンポーネント内で利用するポイント
// const localPoints = ref(props.points);

// Propsのnoteを加工する算出プロパティ
const localNote = computed(
  (): string => {
    let localNote = props.note;
    if (localNote == undefined) {
      localNote = "--";
    }
    return localNote;
  }
)

const onInput = (event: Event): void => {
  const element = event.target as HTMLInputElement;
  const inputPoints = Number(element.value);
  emit("update:points", inputPoints)
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
      <dd>
        <input type="number" v-bind:value="points" v-on:input="onInput">
      </dd>
      <dt>備考</dt>
      <!-- <dd>{{ localNote }}</dd> -->
      <dd>{{ note }}</dd>
    </dl>

    <!-- <button v-on:click="pointUp">ポイント加算</button> -->
  </section>
</template>

<style scoped>
.box {
  border: 1px solid red;
  margin: 10px;
}
</style>
