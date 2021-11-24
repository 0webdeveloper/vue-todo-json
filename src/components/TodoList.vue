<template>
    <div>
        <ul>
           <TodoItem
           v-for="todo in todos"
           :key="todo.title"
           :items="todo"/>
        </ul>
    </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";
import {eventBus} from "../main";

export default {

  props: ['todos'],
  components: {
    TodoItem
  }
}
</script>

<style scoped>
    ul {
        margin: 10px auto;
        list-style: none;
        padding: 0;
    }
</style>