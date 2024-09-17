<template>
  <div class="todoList">
      <h1>TODOリスト</h1>
      <TodoInput @sendErrMsg="showErrMsg" @saveList="updateList"></TodoInput>
      <div class="err-area">{{ err }}</div>
      <TodoListView :key="todoListKey"></TodoListView>
  </div>
</template>
<script setup>
  import TodoInput from "./TodoInput.vue";
  import TodoListView from "./TodoListView.vue";
  import { ref } from "vue";
  const err = ref("");
  let todoListKey = ref(0); // キーを更新することでコンポーネントを再レンダリングする
  localStorage.setItem("message", "ローカルストレージに保存");
  function showErrMsg(message) {
      err.value = message;
  }
  function updateList() {
      todoListKey.value += 1;
  }
</script>
<style>
</style> 