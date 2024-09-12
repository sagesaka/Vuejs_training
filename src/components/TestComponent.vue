<!-- 練習 -->

<!-- 親からデータを受け取る -->
<script setup>
const props = defineProps({
  message: String
})
</script>

<template>
  {{ message }}
</template>


<!-- データバインディング -->

<!-- イベントバインディング(@click="メソッド") -->
<template>
  <button @click="XButtonClick">ボタン</button>
</template>

<script setup>
function XbuttonClick() {
  console.log("クリックされました")
}
</script>

<!-- 双方向バインディング -->
<template>
  <input type="text" id="name" v-model="name" />
  <div>
    入力された名前は: {{ name }}
  </div>
</template>

<script setup>
import { ref } from "vue";
const name = ref("");
</script>

<!-- ref関数で値を宣言するとその値を常に監視し、データが変更されるとすぐに反映する。(DOMと仮想DOMの差分) -->