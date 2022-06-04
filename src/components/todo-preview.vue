<script setup lang="ts">
  import {onMounted, reactive, ref, type Ref} from 'vue'
  interface Todo {
    id: string
    txt: string
    done: boolean
  }

  const props = defineProps({
    todo: Object,
  })

  const emit = defineEmits<{
    (e: 'remove', id: string): void
  }>()

  function toggleDone(): void {
    console.log('todo', props.todo)
    // const todo: Todo | undefined = todos.value.find((t) => t.id === todoId)
    props.todo!.done = !props.todo?.done // to fix Object is possibly 'undefined'
  }

  function removeTodo(todoId: string): void {
    emit('remove', todoId)
  }
</script>
<template>
  <li>
    <pre :class="{done: todo!.done}">{{ todo }}</pre>
    <div class="btns-container">
      <button @click="removeTodo(todo!.id)">Delete</button>
      <button @click="toggleDone()">Done</button>
    </div>
  </li>
</template>
<style scoped></style>
