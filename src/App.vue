<template>
  <div id="app">
    <div class="container">
    <h1>Todolist components</h1>
      <TodoList :todos="arrTodos"/>
  </div>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import {eventBus} from "./main";

export default {
  data() {
    return {
      arrTodos:[
      ]
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then(response => response.json())
          .then(json => {
            this.arrTodos = json
          });
  },
  created() {
    eventBus.$on('remTodo',data => {
      console.log(data)
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
</style>
