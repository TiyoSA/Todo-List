<template>
  <div class="app">
    <h1>To-Do List</h1>

    <form @submit.prevent="addTodo" class="input-section">
      <input v-model="newTodo" placeholder="Tambah kegiatan..." />
      <button type="submit">Tambah</button>
    </form>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="filterIncomplete" />
        Tampilkan yang belum selesai
      </label>
    </div>

    <ul class="todo-table">
      <li v-for="(todo, index) in filteredTodos" :key="index" :class="{ done: todo.done }">
        <div class="col-checkbox">
          <input type="checkbox" v-model="todo.done" />
        </div>
        <div class="col-task">
          <span>{{ todo.text }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTodo = ref('')
const todos = ref([])
const filterIncomplete = ref(false)

function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push({ text: newTodo.value, done: false })
    newTodo.value = ''
  }
}

const filteredTodos = computed(() => {
  return filterIncomplete.value
    ? todos.value.filter(todo => !todo.done)
    : todos.value
})
</script>