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

<!-- 条件分岐 -->
<script setup>
const number = 10;
</script>

<template>
  <div>
    <p v-if="number < 20">
      numberは20よりも小さいです
    </p>
    <p v-else>
      numberは20よりも大きいです
    </p>
  </div>
</template>

<!-- ループ処理 -->
<script setup>
const studentsList = ["山田", "佐藤", "田中"]
</script>

<template>
  <ul>
    <li v-for="student in studentsList" :key="student.id">
      {{ student.name }}
    </li>
  </ul>
</template>

<!-- 要素を一意に識別するために、key属性を付与するべし -->


<!-- 子コンポーネントから親コンポーネントへデータを渡す -->
<template>
  <button @click="sendMessage">メッセージを送る</button>
</template>

<script setup>
import { defineEmits } from "vue";

const emits = defineEmits(["message"]);
const sendMessage = () => {
  emits("message", "子コンポーネントから送ります")
};
</script>

<!-- 親コンポーネント -->
<template>
  <div>
    <child-component @message="handleMessage"></child-component>
    <p>{{ receivedMessage }}</p>
  </div>
</template>

<script setup>
import ChildComponent from "./TestComponent7_child.vue";
import { ref } from "vue";
const receivedMessage = ref("");
 
const handleMessage = (message) => {
  receivedMessage.value = message;
};
</script>