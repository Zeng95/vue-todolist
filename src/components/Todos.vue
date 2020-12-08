<template>
  <div class="todos">
    <ul>
      <li v-for="todo in todos" v-bind:key="todo.id">
        <TodoItem
          v-bind:initialTodo="todo"
          v-on:delete-todo="$emit('delete-todo', todo.id)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import TodoItem from './TodoItem'

export default {
  name: 'Todos',
  props: {
    todos: {
      type: Array,
      default: () => [],
      required: true
    }
  },
  components: { TodoItem }
}
</script>

<style scoped>
.todos {
}
</style>
