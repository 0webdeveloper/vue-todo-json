<template>
  <div>
    <li>
      <div :class="{done: checkbox}">
        <strong>{{index + 1}}</strong>
        <input type="checkbox" v-model="checkbox"/>
        <span>{{items.title}}</span>
      </div>
      <button class="btn" @click="removeTodo">&times;</button>
    </li>
  </div>
</template>

<script>
import {eventBus} from "../main";

export default {
  data() {
    return {
      checkbox: false,
    }
  },
  props: ['items', 'index'],
  methods: {
    removeTodo(id) {
      eventBus.$emit('remTodo', this.items.id)
    }
  }
}
</script>

<style scoped>
li{
  display: flex;
  align-items: center;
  padding: 15px;
  margin-bottom: 18px;
  border-radius: 5px;
  box-shadow: 1px 5px 15px #dfdfdf;
}
li > div{
  display: flex;
  align-items: center;
}
li > div > * {
  margin-right: 10px;
}
input[type="checkbox"] {
  display: inline-block;
  width: 20px;
  height: 20px;
  border: 1px solid #dfdfdf;
  border-radius: 5px;
}
span{
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
  background: #ca9aff;
  cursor: pointer;
  margin-left: auto;
}
.done {
  text-decoration: line-through;
}
</style>