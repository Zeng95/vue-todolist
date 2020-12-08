<template>
  <div class="home">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from '../components/Todos'
import AddTodo from '../components/AddTodo'
import axios from 'axios'

const API_URL = 'https://jsonplaceholder.typicode.com/todos'

export default {
  name: 'Home',
  components: { Todos, AddTodo },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    async getTodos() {
      try {
        const response = await axios.get(`${API_URL}?_limit=10`)

        this.todos = response.data
      } catch (err) {
        console.errr(`Error: ${err.message}`)
      }
    },
    async addTodo(newTodo) {
      try {
        const response = await axios.post(`${API_URL}`, newTodo)

        this.todos = [...this.todos, response.data]
      } catch (err) {
        console.errr(`Error: ${err.message}`)
      }
    },
    async deleteTodo(todoId) {
      try {
        await axios.delete(`${API_URL}/${todoId}`)

        this.todos = this.todos.filter(todo => todo.id !== todoId)
      } catch (err) {
        console.errr(`Error: ${err.message}`)
      }
    }
  },
  created() {
    this.getTodos()
  }
}
</script>
