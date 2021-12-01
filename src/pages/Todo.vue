<template>
  <div>
    <h2>Todolist components</h2>
    <CounterTodo :arrTodos="arrTodos"/>
    <AddForm @add-todo="addTodo"/>
    <Loader v-if="loading"/>
    <TodoList :todos="arrTodos"
              v-else-if="arrTodos.length"/>
    <p v-else>No Todos or all todos is done! Congratulations!</p>
  </div>
</template>


<script>
import TodoList from "@/components/TodoList";
import AddForm from "@/components/AddForm";
import {eventBus} from "@/main";
import CounterTodo from "@/components/CounterTodo";
import Loader from "@/components/PreLoader";


export default {
  data() {
    return {
      arrTodos: [],
      loading: true
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=20')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
            this.arrTodos = json;
            this.loading = false;
          },1000)
        });
  },
  created() {
    eventBus.$on('remTodo', data => {
      this.arrTodos = this.arrTodos.filter((array) => array.id !== data.id);
    });
  },
  methods: {
    addTodo(data) {
      this.arrTodos.push(data)
    }
  },
  components: {
    CounterTodo, TodoList, AddForm, Loader
  }
}
</script>