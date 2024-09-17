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
      <tr v-for="item in items" :key="item.id">
        <td>{{ item.id }}</td>
        <td>
          <span v-if="!item.onEdit">{{ item.content }}</span>
          <input v-else type="text" />
        </td>
        <td>
          <span v-if="!item.onEdit">{{ item.limit }}</span>
          <input v-else type="date" />
        </td>
        <td>
          <span v-if="!item.onEdit">{{ item.state.value }}</span>
          <select v-else v-model="inputState">
            <option
              v-for="state in statuses"
              :key="state.id"
              :value="state"
              :selected="state.id == item.state.id">
              {{ state.value }}
            </option>
          </select>
        </td>
        <td>
          <button>編集</button>
        </td>
        <td>
          <button>削除</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script setup>
import { statuses } from '@/const/status';
// getItemを使ってローカルストレージからデータを取得
const items = JSON.parse(localStorage.getItem("items")) || [];
</script>