<template>
  <div class="app">
    <h1>To-Do List</h1>

    <form @submit.prevent="addTodo" class="input-section">
      <input v-model="newTodo" placeholder="Tambah kegiatan..." />
      <button type="submit">Tambah</button>
    </form>

    <ul class="todo-table">
      <li v-for="(todo, index) in todos" :key="index">
        <div class="col-task">
          <span>{{ todo.text }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTodo = ref('')
const todos = ref([])

function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push({ text: newTodo.value, done: false })
    newTodo.value = ''
  }
}
</script>