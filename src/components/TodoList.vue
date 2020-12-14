<template>
  <ul class="todo-list">
    <todo-item
      v-for="(todo, index) of todos"
      :key="index"
      :todo="todo"
      :index="index"
      @remove-todo="$emit('remove-todo', $event)"
      @edit-todo="$emit('edit-todo', $event)"
      @done-todo-edit="$emit('done-todo-edit', $event)"
      @update-state="$emit('update-state')"
    ></todo-item>
  </ul>
</template>

<script>
import TodoItem from '@/components/TodoItem'

export default {
  props: {
    todos: {
      type: Array,
      required: true
    }
  },
  components: {
    TodoItem
  }
}
</script>