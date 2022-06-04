<script setup lang="ts">
  import {computed, provide, reactive, ref, watchEffect, type Ref} from 'vue'
  import todoList from '../components/todo-list.vue'
  import {todoService} from '../services/todo.service.js'

  const STORAGE_KEY = 'todoDB'

  interface Todo {
    id: string
    txt: string
    done: boolean
    createdAt: number
  }

  // state
  const todoText: Ref<string> = ref('')
  const searchText: Ref<string> = ref('')
  const sortKey: Ref<string> = ref('')
  const todos: Ref<Todo[]> = ref(todoService.query())

  // persist state
  watchEffect(() => {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos.value))
  })

  function makeId(leng = 5) {
    let id = ''
    for (let i = 0; i < leng; i++) {
      id += String.fromCharCode(Math.random() * (127 - 35) + 35)
    }
    return id
  }

  function removeTodo(todoId: string): void {
    const idx = todos.value.findIndex((t) => t.id === todoId)
    const removedTodo = todos.value.splice(idx, 1)[0]
    console.log('removedTodo', removedTodo)
  }

  function addTodo(txt: string): void {
    if (!txt) return
    const todo = {
      id: makeId(),
      txt,
      done: false,
      createdAt: Date.now(),
    }
    todos.value.push(todo)
  }

  function filter() {
    todosToShow
  }

  const todosToShow = computed(() => {
    if (searchText.value) {
      return todos.value.filter((t) => t.txt.includes(searchText.value))
    }
    const key = sortKey.value
    if (key) {
      return todos.value.sort((a, b) => {
        a = a[key]
        b = b[key]
        return a === b ? 0 : a > b ? 1 : -1
      })
    }
    return todos.value
  })

  function sortBy(key: string) {
    sortKey.value = key
  }

  const darkMode = ref(false)
  const toggleDarkMode = () => {
    darkMode.value = !darkMode.value
    const elBody = document.querySelector('body')
    darkMode.value
      ? (elBody!.style.backgroundColor = 'black')
      : (elBody!.style.backgroundColor = 'white')
  }

  provide('dark-mode', darkMode)
</script>

<template>
  <div class="greetings">
    <button @click="toggleDarkMode">Toggle theme</button>
    <h1>Hi Todos</h1>

    <input
      type="text"
      placeholder="search"
      @input="filter"
      v-model="searchText"
    />
    <input type="text" v-model="todoText" />

    <button @click="addTodo(todoText)">Add Todo</button>
    <button @click="sortBy('txt')">Sort by name</button>
    <button @click="sortBy('createdAt')">Sort by date</button>
    <todoList @remove="removeTodo" :todos="todosToShow" />
  </div>
</template>

<style scoped></style>
