<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Header />
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodoItem"/>
  </div>
</template>

<script>
import Todos from '../components/Todos'
import Header from '../components/layouts/Header'
import AddTodo from '../components/AddTodo'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Todos,
    Header,
    AddTodo
  },
  methods: {
    deleteTodoItem(todoItemId){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${todoItemId}`).
      then(response => {
              console.log(response);
              this.todos = this.todos.filter(todo => todo.id !== todoItemId)
      }).catch(err => console.log(err))
    },
    addTodo(newTodoItem){
      axios.
      post('https://jsonplaceholder.typicode.com/todos', newTodoItem).
      then(response => this.todos = [...this.todos, response.data]).catch(err => console.log(err))
    },
    fetchTodos(){
      axios.
      get('https://jsonplaceholder.typicode.com/todos?_limit=5').
      then(response => this.todos = response.data).catch(err => console.log(err))
    }
  },
  data() {
    return {
      todos: []
    }
  },
  created() {
    this.fetchTodos()
  }
}
</script>
