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
  <div class="box_list">
    <div class="todo_list" v-for="todo in todoListRef" :key="todo.id">
      <div class="todo">
        <input type="checkbox" class="check" />
        <label>{{ todo.task }}</label>
      </div>
      <div class="btns">
        <button class="btn green">編</button>
        <button class="btn pink">削</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// テキストボックスに入力された内容を受け取る
const todoRef = ref('');

// テキストボックスに入力された内容をリストで格納する用
// ローカルストレージにtodoListがいればそれを格納し、なければ空配列で初期化
const todoListRef = ref([]);
const ls = localStorage.todoList;
todoListRef.value = ls ? JSON.parse(ls) : [];

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

.box_list {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.todo_list {
  display: flex;
  align-items: center;
  gap: 8px;
}

.todo {
  border: 1px solid #ccc;
  border-radius: 6px;
  padding: 12px;
  width: 300px;
}

.check {
  border: 1px solid red;
  transform: scale(1.6);
  margin: 0 16px 2px 6px;
}

.btns {
  display: flex;
  gap: 4px;
}

.green {
  background-color: #00c853;
}

.pink {
  background-color: #ff4081;
}
</style>
