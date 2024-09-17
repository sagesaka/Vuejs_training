<template>
  
</template>

<script setup>
// getItemを使ってローカルストレージからデータを取得
const items = JSON.parse(localSttorage.geItem("items")) || [];
</script>