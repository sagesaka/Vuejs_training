<template>
  <div>
    <form action="">
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

const input = ref("");
const inputDate = ref("");
</script>