<script setup lang="ts">
  import {inject, reactive, ref, type Ref} from 'vue'
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

  const darkMode = inject<Ref<boolean>>('dark-mode')
</script>
<template>
  <ul>
    <todoPreview
      :class="{dark: darkMode}"
      @remove="(todoId) => emit('remove', todoId)"
      v-for="todo in todos"
      :todo="todo"
      :key="todo.id"
    />
  </ul>
</template>
<style scoped></style>
