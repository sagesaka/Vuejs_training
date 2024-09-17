<template>
  <div class="input-area">
    <form @submit.prevent="onClickBtn">
      <label class="input-label"
        >やること<input type="text" class="input" v-model="input" /></label
      ><br />
      <label class="input-label"
        >期限<input type="date" class="input" v-model="inputDate" /></label
      ><br />
      <input type="submit" class="submit-btn btn" value="登録！" />
    </form>
  </div>
</template>
<script setup>
import { ref } from "vue";
import { defineEmits } from "vue";
const input = ref("");
const inputDate = ref("");
const stateList = [
  { id: 0, value: "未実施" },
  { id: 1, value: "実行中" },
  { id: 2, value: "完了" },
];
const emit = defineEmits(["SendErrMsg", "saveList"]);
 
function onClickBtn() {
  if (!input.value) {
    emit("SendErrMsg", "やることを入力してください");
    return;
  }
 
  emit("SendErrMsg", "");
  //更新前に現在の状況を取得する
 
  const items = JSON.parse(localStorage.getItem("items")) || [];
 
  //期限は入力がなかった場合は空
  items.push({
    id: items.length,
    value: input.value,
    limit: inputDate.value || "",
    state: stateList[0],
    onEdit: false,
  });
  input.value = "";
  saveList(items);
}
function saveList(items) {
  localStorage.setItem("items", JSON.stringify(items));
  items = JSON.parse(localStorage.getItem("items"));
  //テーブルの表示を更新するために親コンポーネントへイベントを送る
  emit("saveList");
}
</script>