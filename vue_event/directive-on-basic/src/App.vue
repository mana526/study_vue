<script setup lang="ts">
import { ref } from "vue";

// ①
const randValue = ref("まだです");
const onButtonClick = (): void => {
  const rand = Math.round(Math.random() * 10);
  randValue.value = String(rand);
}

// ②
const mousePointerX = ref(0);
const mousePointerY = ref(0);
const onImgMousemove = (event: MouseEvent): void => {
  mousePointerX.value = event.offsetX;
  mousePointerY.value = event.offsetY;
}

// ③
const pBgColor = ref("white");
const onPClick = (bgColor: string): void => {
  pBgColor.value = bgColor;
}

// ④
const pMsg = ref('ここをクリック！');
const pBgColorEvent = ref('white');
const onPClickEvent = (bgColor: string, event: MouseEvent): void => {
  pBgColorEvent.value = bgColor;
  pMsg.value = event.timeStamp;
}
</script>

<template>
  <div class="wrap">
    <!--　①基本のイベントリスナの設定。onButtonClickのところは処理そのものでないといけない。 -->
    <section class="first">
      <h1>基本のv-onディレクティブ</h1>
      <button v-on:click="onButtonClick">クリック</button>
      <p>クリックの結果：{{ randValue }}</p>
    </section>

    <!-- ②v-onディレクティブに対応したイベントハンドラメソッドは、イベントオブジェクトを引数として受け取ることができる。 -->
     <section class="second">
      <h1>イベントオブジェクトを引数として受け取る</h1>
      <img src="./assets/logo.svg" alt="" v-on:mousemove="onImgMousemove">
      <p>ポインタの位置: x={{ mousePointerX }}; y={{ mousePointerY }}</p>
     </section>

    <!-- ③イベントオブジェクト以外を引数とするイベントハンドラメソッド -->
     <section class="third">
      <h1>イベントオブジェクト以外の引数</h1>
      <p v-on:click="onPClick('red')" v-bind:style="{backgroundColor: pBgColor}">
        ここをクリックすると背景色が変わります。
      </p>
     </section>

    <!-- ④イベントオブジェクトとそのほかの引数を併用するイベントハンドラメソッド -->
     <section class="forth">
        <h1>イベントオブジェクトとそれ以外の引数の併用</h1>
        <p v-on:click="onPClickEvent('green', $event)" v-bind:style="{backgroundColor: pBgColorEvent}">
          {{ pMsg }}
        </p>
     </section>
  </div>
</template>

<style scoped>
.wrap {
  width: 80vw;
  margin: 0 auto;
}

.first {
  margin: 100px 0;
}

.second img{
  width: 20%;
}

.third {
  cursor: pointer;
  margin: 100px 0;
}

.forth {
  cursor: pointer;
}
</style>
