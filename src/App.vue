<template>
  <div id="app">
    <div class="container">
    <h1>Todolist components</h1>
    <hr>
    <div class="counter-todo">
      <span>number of todos</span>
      <b class="counter-todo_numer">{{ count }}</b>
    </div>
      <TodoList :todos="arrTodos"
 />

  </div>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import {eventBus} from "./main";

export default {
  data() {
    return {
      arrTodos:[],
      count: 0
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
          .then(json => {
            this.arrTodos = json;
            this.count = json.length;
          });
  },
  created() {
    eventBus.$on('remTodo', data => {
     this.arrTodos = this.arrTodos.filter((t) => t.id !== data);
     this.count = this.arrTodos.length;
    });
  },
  components: {
    TodoList
  }
}
</script>

<style>
*{
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
}
.counter-todo{
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px auto;
}
.counter-todo_numer{
  margin-left: 10px;
  font-size: 1.2em;
  color: #cc0000;
}
</style>
