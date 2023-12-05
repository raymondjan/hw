<script setup>
import { ref } from 'vue'

let id = 0

const title = "Todo list"

const newTodo = ref('')

const todos = ref([
  { id: id++, text: 'todo1', done: true },
  { id: id++, text: 'todo2', done: true },
  { id: id++, text: 'todo3', done: true }

])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <div>
    <h1 class="title">{{ title }}</h1>
    <p>for study todo app</p>
    <form @submit.prevent="addTodo">
      <input v-model="newTodo" placeholder="做點重要的事情..." style="font-size: 26px; width: 60%;" />
      <button style="font-size: 26px; width: 10%;">新增</button>
    </form>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <input type="checkbox" v-model="todo.done">
        <span :class="{ done: todo.done }" style="font-size: 26px;">{{ todo.text }}</span>
        <button @click="removeTodo(todo)" style="font-size: 26px;">X</button>
      </li>
    </ul>
  </div>
</template>

<style>
.title {
  font-size: 48px; 
}

form, ul {
  font-size: 26px; 
}

.done {
  text-decoration: line-through;
}
</style>
