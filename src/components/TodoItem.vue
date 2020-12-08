<template>
  <div class="todo-item">
    <div class="form-group" v-bind:class="{ 'is-completed': todo.completed }">
      <input type="checkbox" v-bind:id="todo.id" v-model="todo.completed" />
      <label v-bind:for="todo.id">{{ todo.title }}</label>
    </div>
    <button class="btn-delete" v-on:click="$emit('delete-todo', todo.id)">
      X
    </button>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    initialTodo: {
      type: Object,
      default: () => {},
      required: true
    }
  },
  data() {
    return {
      todo: this.initialTodo
    }
  }
}
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-completed {
  text-decoration: line-through;
}

.form-group {
  display: flex;
  align-items: center;
}

.form-group > label {
  margin-left: 1rem;
}

.btn-delete {
  padding: 0.4rem;
  background-color: rgba(255, 0, 0, 0.5);
  color: #fff;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  font-size: 12px;
  transition: background-color 0.3s;
}

.btn-delete:hover {
  background-color: rgba(255, 0, 0, 1);
}
</style>
