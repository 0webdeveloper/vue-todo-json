<template>
  <div>
    <h2>Todolist components</h2>

    <div class="counter-todo">
      <span>number of todos <b class="counter-todo_number">{{ quantity }} </b></span>
      <span class="counter-todo_completed">{{ checkCompleted }} (done)</span>
    </div>

    <AddForm @add-todo="addTodo"/>

    <p class="filter-title">Todo filter</p>
    <select class="filterTodo" v-model="filter">
      <option v-for="value in select" :value="value">{{ value }}</option>
    </select>

    <Loader v-if="loading"/>
    <TodoList :todos="filterTodos"
              v-else-if="filterTodos.length"/>
    <p v-else>No Todos or all todos is done! Congratulations!</p>
  </div>
</template>


<script>
import TodoList from "@/components/TodoList";
import AddForm from "@/components/AddForm";
import {eventBus} from "@/main";
import Loader from "@/components/PreLoader";


export default {
  data() {
    return {
      arrTodos: [

      ],
      loading: true,
      select: ['all', 'completed', 'active'],
      filter: 'all',
      count: null,
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
        .then(response => response.json())
        .then(json => {
          this.arrTodos = json;
          this.loading = false;
        });
  },
  computed: {
    filterTodos() {
      if (this.filter === 'all') {
        return this.arrTodos;
      }
      if (this.filter === 'completed') {
        return this.arrTodos.filter(item => item.completed);
      }
      if (this.filter === 'active') {
        return this.arrTodos.filter(item => !item.completed);
      }
    },
    checkCompleted() {
      let sum = 0;
      this.arrTodos.forEach(item => {
        if (item.completed) {
          sum++
        }
      });
      return sum;
    },
    quantity() {
      return this.arrTodos.length;
    }
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
    TodoList, AddForm, Loader
  }
}
</script>

<style lang="scss">
.filter-title {
  margin-bottom: 20px;
}

.filterTodo {
  display: block;
  font: 700 16px sans-serif;
  color: #444;
  line-height: 1.3;
  outline: none;
  padding: 10px;
  width: 100%;
  max-width: 100%;
  box-sizing: border-box;
  margin-bottom: 30px;
  border: 1px solid #aaa;
  box-shadow: 0 1px 0 1px rgba(0, 0, 0, .04);
  border-radius: 5px;
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  background-color: #fff;
  background-image: url(data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23007CB2%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E), linear-gradient(to bottom, #ffffff 0%, #e5e5e5 100%);
  background-repeat: no-repeat, repeat;
  background-position: right .7em top 50%, 0 0;
  background-size: .65em auto, 100%;
}

.counter-todo {
  margin: 20px auto;
}

.counter-todo_number {
  color: #7fff00;
}

.counter-todo_completed {
  display: block;
  margin: 10px auto;
}

</style>