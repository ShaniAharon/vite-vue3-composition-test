<script setup lang="ts">
  import {reactive, ref, type Ref} from 'vue'

  interface Todo {
    id: number
    txt: string
    completed: boolean
  }

  const count: Ref<number> = ref(0)
  const todos = ref([
    {id: 0, txt: 'just do it', completed: false},
    {id: 1, txt: 'yes you can', completed: false},
  ])
  function increment() {
    count.value++
  }
</script>

<template>
  <div class="greetings">
    <h1>Hi Todos</h1>
    <h3>{{ count }}</h3>
    <button @click="increment">Increment</button>

    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <pre>{{ todo }}</pre>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
