<template>
  <form class="todo-form" @submit.prevent="addTodo">
    <input class="todo-form_input" type="text" placeholder="addTodo" v-model="title"/>
    <button class="todo-form_button">add todo</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo() {
      const newTodo = {
        id: Date.now(),
        title: this.title,
        completed: false
      }
      this.$emit('add-todo', newTodo);
      this.title = '';
    }
  }
}
</script>

<style scoped>
.todo-form{
  display: flex;
  align-items: center;
  margin-bottom: 50px;
}
.todo-form_input {
  padding: 15px;
  width: 100%;
  border: 1px solid #d4d4d4;
  border-radius: 5px;
}
.todo-form_button {
  display: inline-block;
  padding: 15px;
  border-radius: 5px;
  border: none;
  color: #fff;
  background-color: goldenrod;
  width:10%;
  margin-left: 15px;
  transition: background .2s ease-in-out;
  text-transform: uppercase;
  cursor: pointer;
}
.todo-form_button:hover {
  background-color: #b38404;
}
</style>