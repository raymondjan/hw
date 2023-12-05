<script setup>

import { ref} from 'vue'

let id = 0

const title = "Todo list"

const newTodo = ref('')

 

const todos = ref([

  { id: id++, text: 'TEST', done: true },

  { id: id++, text: 'TEST2', done: true },

  { id: id++, text: 'TEST3', done: false }

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

  <h1 class="title">{{ title }}</h1>

  <form @submit.prevent="addTodo">

    <input v-model="newTodo" placeholder="Do something...">

    <button>Add Todo</button>

  </form>

  <ul>

    <li v-for="todo in todos" :key="todo.id">

      <input type="checkbox" v-model="todo.done" >

      <span :class="{ done: todo.done }">{{ todo.text }}</span>

      <button @click="removeTodo(todo)">X</button>

    </li>

  </ul>

 

</template>

 

<style>

.done {

  text-decoration: line-through;

}

</style>
