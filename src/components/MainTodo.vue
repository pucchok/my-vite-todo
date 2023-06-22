<template>
  <div class="box_input">
    <input
      type="text"
      class="todo_input"
      placeholder="+ TODOを入力"
      v-model="todoRef"
    />
    <button class="btn" @click="addTodo">追加</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// テキストボックスに入力された内容を受け取る
const todoRef = ref('');

// テキストボックスに入力された内容をリストで格納する用
const todoListRef = ref([]);

const addTodo = () => {
  // idとしてミリ秒を使う
  const id = new Date().getTime();

  // todoListRefの中にid:todo内容を格納
  todoListRef.value.push({ id: id, task: todoRef.value });

  // ローカルストレージに入力値を格納する
  localStorage.todoList = JSON.stringify(todoListRef.value);

  // 格納後に入力値は空にする
  todoRef.value = '';
};
</script>

<style scoped>
.box_input {
  margin-top: 20px;
}

.todo_input {
  width: 300px;
  margin-right: 8px;
  padding: 8px;
  font-size: 18px;
  border: 1px solid #aaa;
  border-radius: 6px;
}

.btn {
  padding: 8px;
  background-color: #03a9f4;
  border-radius: 6px;
  color: #fff;
  text-align: center;
  font-size: 14px;
}
</style>
