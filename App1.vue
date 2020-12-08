<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from './components/layout/Header'
import Todos from './components/Todos'
import AddTodo from './components/AddTodo'
import axios from 'axios'

const API_URL = 'https://jsonplaceholder.typicode.com/todos'

export default {
  name: 'App',
  components: { Header, Todos, AddTodo },
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
    async deleteTodo(id) {
      try {
        await axios.delete(`${API_URL}/${id}`)

        this.todos = this.todos.filter(todo => todo.id !== id)
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

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.5;
}

button,
input {
  outline: none;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
