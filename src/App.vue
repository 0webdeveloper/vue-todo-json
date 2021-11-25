<template>
  <div id="app">
    <div class="container">
      <h1>Todolist components</h1>
      <CounterTodo :arrTodos="arrTodos"/>
      <AddForm/>
      <TodoList :todos="arrTodos"/>
    </div>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddForm from "@/components/AddForm";
import {eventBus} from "./main";
import CounterTodo from "./components/CounterTodo";

export default {
  data() {
    return {
      arrTodos: [],
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=7')
        .then(response => response.json())
        .then(json => {
          this.arrTodos = json;
        });
  },
  created() {
    eventBus.$on('remTodo', data => {
      this.arrTodos = this.arrTodos.filter((array) => array.id !== data.id);
    });
  },
  components: {
    CounterTodo,
    TodoList, AddForm
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 1.2em;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}
</style>
