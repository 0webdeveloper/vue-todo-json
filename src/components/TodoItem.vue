<template>
  <div>
    <li>
      <div :class="{done: items.completed}">
        <input type="checkbox" v-model="items.completed"/>
        <strong>{{ index + 1 | startZero}}</strong>
        <span>{{ items.title | upperCase}}</span>
      </div>
      <button class="btn" @click="removeTodo">&times;</button>
    </li>
  </div>
</template>

<script>
import {eventBus} from "../main";

export default {
  data() {
    return {}
  },
  props: ['items', 'index'],
  methods: {
    removeTodo(id) {
      eventBus.$emit('remTodo', {
        id: this.items.id,
        completed: this.items.completed
      })
    }
  },
  filters: {
    upperCase(value) {
    return value.toUpperCase();
    },
    startZero(id) {
      if(id < 10) {
        id = '0' + id
      }
      return id;
    }
  }
}
</script>

<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  padding: 15px;
  margin-bottom: 18px;
  border-radius: 5px;
  background-color: #fff;
  color: #2c3e50;

  & > div {
    display: flex;
    align-items: center;

    & > * {
      margin-right: 10px;
    }
  }
}

input[type="checkbox"] {
  display: inline-block;
  width: 20px;
  height: 20px;
  border: 1px solid #dfdfdf;
  border-radius: 5px;
}

span {
  text-align: left;
}

.btn {
  display: block;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  border: none;
  color: #fff;
  font-size: 1.2em;
  background: #CC92C2;
  cursor: pointer;
  margin-left: auto;
}

.done {
  text-decoration: line-through;
  color: #cc0000;
}
</style>