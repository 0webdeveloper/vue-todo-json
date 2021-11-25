<template>
  <div id="app">
    <div class="container">
    <h1>Todolist components</h1>
    <hr>
    <div class="counter-todo">
      <span>number of todos</span>
      <b class="counter-todo_numer">{{ count }} </b>
      <span> / {{ checkCompleted() }} (done)</span>
    </div>
      <AddForm />
      <TodoList :todos="arrTodos" />

  </div>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddForm from "@/components/AddForm";
import {eventBus} from "./main";

export default {
  data() {
    return {
      arrTodos:[],
      count: 0,
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then(response => response.json())
          .then(json => {
            this.arrTodos = json;
            this.count = json.length;
          });
  },
  created() {
    eventBus.$on('remTodo', data => {
     this.arrTodos = this.arrTodos.filter((array) => array.id !== data.id);
     this.count = this.arrTodos.length;
     this.completed = this.checkCompleted();
    });
  },
  methods: {
    checkCompleted() {
      let sum = 0;
      this.arrTodos.forEach(item => {
          if(item.completed === true) {
            sum += 1
          }
      });
      return sum;
    }
  },
  components: {
    TodoList, AddForm
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
