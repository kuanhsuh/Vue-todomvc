<template>
  <div class="hello">
    <h1>TodoMVC</h1>
    <input text="submit" v-model="input"/>
    <button @click="addTodo">Add Todo</button>
    <div>{{input}}</div>
    <ul>
      <li v-for="todo in todos">
        <input class="toggle" type="checkbox" v-model="todo.completed">
        {{todo.text}} <button @click="deleteTodo(todo.id)">x</button><button @click="showUpdateTodo(todo)">update</button>
        <input type="text" 
          v-if="todo.updateInput" 
          v-model="todo.text">
        </input>
      </li>
    </ul>
    <button @click="allComplete">All Complete</button>
    <button @click="clearComplete">Clear All Complete</button>
    <button @click="deleteAllTodo">Delete All</button>
  </div>
</template>

<script>
// import _ from 'lodash'
export default {
  name: 'hello',
  data () {
    return {
      input: '',
      todos: [
        {
          id: 1,
          text: 'Learn vue',
          updateInput: true,
          completed: false
        },
        {
          id: 2,
          text: 'Learn css',
          updateInput: false,
          completed: true
        }
      ]
    }
  },
  methods: {
    addTodo: function (e) {
      e.preventDefault()
      var newTodo = {
        id: this.todos.length + 1,
        text: this.input,
        updateInput: false,
        completed: false
      }
      this.todos.push(newTodo)
      this.input = ''
    },
    deleteTodo: function (id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    showUpdateTodo: function (todo) {
      todo.updateInput = !todo.updateInput
    },
    allComplete: function () {
      this.todos.forEach((todo) => {
        todo.completed = true
      })
    },
    clearComplete: function () {
      this.todos.forEach((todo) => {
        todo.completed = false
      })
    },
    deleteAllTodo: function () {
      this.todos = []
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

a {
  color: #42b983;
}
</style>
