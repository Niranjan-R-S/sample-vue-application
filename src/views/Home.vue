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

export default {
  name: 'Home',
  components: {
    Todos,
    Header,
    AddTodo
  },
  methods: {
    deleteTodoItem(todoItemId){
      this.todos = this.todos.filter(todo => todo.id !== todoItemId)
    },
    addTodo(newTodoItem){
      this.todos = [...this.todos, newTodoItem]
    }
  },
  data() {
    return {
      todos: [
        {
          id:1,
          title: "Todo 1",
          completed: false
        },
        {
          id:2,
          title: "Todo 2",
          completed: true
        },
        {
          id:3,
          title: "Todo 3",
          completed: false
        }
      ]
    }
  }
}
</script>
