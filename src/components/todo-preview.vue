<script setup lang="ts">
  import {inject, onMounted, reactive, ref, type Ref} from 'vue'
  interface Todo {
    id: string
    txt: string
    done: boolean
  }

  const props = defineProps({
    todo: Object,
    msg: String,
  })

  const emit = defineEmits<{
    (e: 'remove', id: string): void
  }>()

  const darkMode = inject<Ref<boolean>>('dark-mode')

  function toggleDone(): void {
    // const todo: Todo | undefined = todos.value.find((t) => t.id === todoId)
    props.todo!.done = !props.todo?.done // to fix Object is possibly 'undefined'
  }

  function removeTodo(todoId: string): void {
    emit('remove', todoId)
  }
</script>
<template>
  <li>
    <pre :class="{done: todo!.done, dark:darkMode}">{{ todo }}</pre>
    <div class="btns-container">
      <button @click="removeTodo(todo!.id)">Delete</button>
      <button @click="toggleDone()">Done</button>
    </div>
  </li>
</template>
<style scoped></style>
