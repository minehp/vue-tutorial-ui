<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import axios from 'axios';
import Todos from "../components/Todos";
import AddTodo from "../components/addTodo";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    async addTodo(newTodo) {
      // const { title, completed } = newTodo;
      // const res = await axios.post('https://jsonplaceholder.typicode.com/todos', {
      //   title,
      //   completed
      // });
      // console.log(res.data);
      this.todos = [newTodo, ...this.todos];
    }
  },
  async created() {
    const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5');
    this.todos = res.data;
  }
};
</script>
