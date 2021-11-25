<template>
  <div class="counter-todo">
    <span>number of todos <b class="counter-todo_number">{{ quantity() }} </b></span>
    <span class="counter-todo_completed">{{ checkCompleted() }} (done)</span>
  </div>
</template>

<script>
export default {
  props: ['arrTodos'],
  data() {
    return {
      count: 0
    }
  },
  methods: {
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
      return this.arrTodos.length
    }
  }
}
</script>

<style scoped>
.counter-todo {
  margin: 20px auto;
}

.counter-todo_number{
  color: #cc0000;
}
.counter-todo_completed{
  display: block;
  margin: 10px auto;
}
</style>