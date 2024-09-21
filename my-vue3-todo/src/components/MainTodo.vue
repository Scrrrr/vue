<script setup lang="ts">
import { ref } from 'vue';

const todo = ref('');

const todoList = ref<{ id: number; task: string }[]>([
  { id: 1, task: 'TODO1' },
  { id: 2, task: 'TODO2' },
  { id: 3, task: 'TODO3' }
]);

const addTodo = () => {
  //idはミリ秒から取得して登録
  const id = new Date().getTime();

  //配列にデータを格納
  todoList.value.push({ id: id, task: todo.value });

  //JSONファイルにシリアライズ化
  localStorage.todoList = JSON.stringify(todoList.value);

  todo.value = '';
};
//script
</script>

<template>
  <div>
    <input type="text" class="todo_input" v-model="todo" placeholder=" + TODOを入力" />
    <button class="btn" @click="addTodo">追加</button>

    <div class="todo_list" v-for="todo in todoList" :key="todo.id">
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

<style scoped>
.box_list {
  display: flex;
  flex-direction: column;
  gap: 4px;
  margin-top: 20px;
}

.todo_list {
  display: flex;
  gap: 8px;
  align-items: center;
}

.todo {
  width: 250px;
  padding: 6px 8px;
  border: 1px solid #ccc;
  border-radius: 6px;
}

.check {
  margin-right: 12px;
  transform: scale(1.6);
}

.todo_input {
  width: 250px;
  padding: 6px 8px;
  margin-right: 8px;
  font-size: 18px;
  border: 1px solid #aaa;
  border-radius: 6px;
}

.btn {
  position: relative;
  padding: 6px 8px;
  font-size: 14px;
  color: #fff;
  text-align: center;
  background-color: #03a9f4;
  border: 1px solid #eee;
  border-radius: 6px;
}

.btn:active {
  top: 1px;
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
