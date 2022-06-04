<script setup lang="ts">
  import {reactive, ref, type Ref} from 'vue'

  interface Todo {
    id: string
    txt: string
    done: boolean
  }

  const todoText: Ref<string> = ref('')
  const todos = ref([
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
</script>

<template>
  <div class="greetings">
    <h1>Hi Todos</h1>

    <input type="text" v-model="todoText" />
    <button @click="addTodo(todoText)">Add Todo</button>

    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <pre>{{ todo }}</pre>
        <div class="btns-container">
          <button @click="removeTodo(todo.id)">Delete</button>
          <button>Edit</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
