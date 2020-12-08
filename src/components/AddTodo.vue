<template>
  <form v-on:submit="addTodo">
    <div class="form-group">
      <input type="text" v-model="title" placeholder="Add Todo..." />
    </div>

    <div class="form-group">
      <button type="submit" class="btn-submit">Submit</button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'AddTodo',
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo(e) {
      e.preventDefault()

      if (this.title === '') return false

      const newTodo = {
        title: this.title,
        completed: false
      }

      this.$emit('add-todo', newTodo)
      this.title = ''
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
}

.form-group:first-of-type {
  flex: 10;
}

.form-group:nth-of-type(2) {
  flex: 2;
}

input[type='text'],
button[type='submit'] {
  width: 100%;
  height: 100%;
}

input[type='text'] {
  text-indent: 10px;
}

.btn-submit {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn-submit:hover {
  background: #666;
}
</style>
