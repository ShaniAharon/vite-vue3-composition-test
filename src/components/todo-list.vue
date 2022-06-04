<script setup lang="ts">
  import {reactive, ref, type Ref} from 'vue'
  import todoPreview from '../components/todo-preview.vue'

  interface Todo {
    id: string
    txt: string
    done: boolean
  }

  const props = defineProps({
    todos: Object,
  })

  const emit = defineEmits<{
    (e: 'remove', id: string): void
  }>()
</script>
<template>
  <ul>
    <todoPreview
      @remove="(todoId) => emit('remove', todoId)"
      v-for="todo in todos"
      :todo="todo"
      :key="todo.id"
    />
  </ul>
</template>
<style scoped></style>
