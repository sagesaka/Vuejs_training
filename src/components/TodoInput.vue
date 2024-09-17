<template>
  <div>
    <form @submit="onSubmitForm">
      <label>
        やること<input type="text" v-model="input"/>
      </label>
      <label>
        期限<input type="date" v-model="inputDate"/>
      </label>
      <input type="submit" value="登録" />
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { statuses } from "@/const/status";

const input = ref("");
const inputDate = ref("");

function onSubmitForm() {
  console.log(input.value)
}
</script>