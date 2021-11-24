<template>
    <div>
        <ul>
           <TodoItem
           v-for="(todo,i) in todos"
           :key="todo.title"
           :index="i"
           :items="todo"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";

export default {

  props: ['todos'],
  components: {
    TodoItem
  },
}
</script>

<style scoped>
    ul {
        margin: 10px auto;
        list-style: none;
        padding: 0;
    }
</style>