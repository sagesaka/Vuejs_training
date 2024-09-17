<template>
  <div>
    <table>
      <tr>
        <th class="th-id">ID</th>
        <th class="th-value">やること</th>
        <th class="th-limit">期限</th>
        <th class="th-state">状態</th>
        <th class="th-edit">編集</th>
        <th class="th-delete">削除</th>
      </tr>
    </table>
  </div>
</template>

<script setup>
// getItemを使ってローカルストレージからデータを取得
const items = JSON.parse(localSttorage.geItem("items")) || [];
</script>