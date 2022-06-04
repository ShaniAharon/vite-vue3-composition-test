<script setup lang="ts">
  import {provide, reactive, ref, type Ref} from 'vue'
  import todoList from '../components/todo-list.vue'

  interface Todo {
    id: string
    txt: string
    done: boolean
  }

  const todoText: Ref<string> = ref('')
  const todos: Ref<Todo[]> = ref([
    {id: makeId(), txt: 'just do it', done: false},
    {id: makeId(), txt: 'yes you can', done: false},
  ])

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
    const todo = {
      id: makeId(),
      txt,
      done: false,
    }
    todos.value.push(todo)
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

    <input type="text" v-model="todoText" />
    <button @click="addTodo(todoText)">Add Todo</button>
    <todoList @remove="removeTodo" :todos="todos" />
  </div>
</template>

<style scoped></style>
