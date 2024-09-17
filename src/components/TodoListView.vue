<template>
  <div class="list-area">
    <!-- 確認モーダル -->
    <div v-if="isConfirmationModalVisible" class="modal">
      <div class="modal-content">
        <p>{{ deleteItemTask }}を削除してもよろしいですか？</p>
        <button @click="deleteItem">はい</button>
        <button @click="hideConfirmationModal">キャンセル</button>
      </div>
    </div>
    <table class="table">
      <thead v-pre>
        <tr>
          <th class="th-id">ID</th>
          <th class="th-value">やること</th>
          <th class="th-limit">期限</th>
          <th class="th-state">状態</th>
          <th class="th-edit">編集</th>
          <th class="th-delete">削除</th>
        </tr>
      </thead>
      <tr v-for="item in items" :key="item.id">
        <td>{{ item.id }}</td>
        <td>
          <span v-if="!item.onEdit">{{ item.value }}</span
          ><span v-else
            ><input
              type="text"
              class="input"
              v-model="newInput"
              :placeholder="item.value"
          /></span>
        </td>
        <td>
          <span v-if="!item.onEdit">{{ item.limit }}</span
          ><span v-else
            ><input
              type="date"
              class="input"
              v-model="newInputDate"
              :placeholder="item.limit"
          /></span>
        </td>
        <td>
          <span v-if="!item.onEdit">{{ item.state.value }}</span>
          <span v-else
            ><select v-model="inputState" class="select">
              <option
                v-for="state in stateList"
                :key="state.id"
                :value="state.id"
                :selected="state.id == item.state.id"
              >
                {{ state.value }}
              </option>
            </select></span
          >
        </td>
        <td>
          <button v-if="!item.onEdit" @click="onEdit(item.id)" class="btn">
            編集</button
          ><button v-else @click="onCompleteEdit(item.id)" class="btn">
            完了
          </button>
        </td>
        <td>
          <button @click="showConfirmationModal(item.id)" class="btn">
            削除
          </button>
        </td>
      </tr>
    </table>
  </div>
</template>
<script setup>
import { ref } from "vue";
//itemsを更新したときに反映されるようにrefを使う
let items = ref(JSON.parse(localStorage.getItem("items")));
if (!items) {
  items = [];
}
const stateList = [
  { id: 0, value: "未実施" },
  { id: 1, value: "実行中" },
  { id: 2, value: "完了" },
];
let newInput = ref("");
let newInputDate = ref("");
let inputState = ref("");
let deleteItemTask = ref("");
let isConfirmationModalVisible = ref(false);
let deleteId = "";
function showConfirmationModal(id) {
  // 確認モーダルを表示
  isConfirmationModalVisible.value = true;
  deleteId = id;
  deleteItemTask = items.value[id].value;
}
function hideConfirmationModal() {
  // 確認モーダルを非表示
  isConfirmationModalVisible.value = false;
}
function deleteItem() {
  items.value.splice(deleteId, 1);

  //idを付け直す
  items.value = items.value.map((item, index) => ({
    id: index,
    value: item.value,
    limit: item.limit,
    state: item.state,
    onEdit: item.onEdit,
  }));

  saveList(items.value);

  // 確認モーダルを非表示
  isConfirmationModalVisible.value = false;
}

function onEdit(id) {
  console.log("edit" + id);
  //初期値にもとの値を入れる
  newInput = items.value[id].value;
  newInputDate = items.value[id].limit;
  inputState = items.value[id].state.id;
  updateList(id, {
    id: id,
    value: items.value[id].value,
    limit: items.value[id].limit,
    state: items.value[id].state,
    onEdit: !items.value[id].onEdit,
  });
}
function onCompleteEdit(id) {
  //入力がなかったらそのまま
  if (!newInput) {
    newInput = items.value[id].value;
  }
  if (!newInputDate) {
    newInputDate = items.value[id].limit;
  }
  updateList(id, {
    id: id,
    value: newInput,
    limit: newInputDate,
    state: stateList[inputState],
    onEdit: !items.value[id].onEdit,
  });
  newInput = "";
  newInputDate = "";
  inputState = "";
}
function updateList(id, item) {
  items.value.splice(id, 1, item);
  saveList(items.value);
}
function saveList(items) {
  localStorage.setItem("items", JSON.stringify(items));
  const JSONItems = localStorage.getItem("items");
  items.value = JSONItems ? JSON.parse(JSONItems) : [];
}
</script>
<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
}
</style>