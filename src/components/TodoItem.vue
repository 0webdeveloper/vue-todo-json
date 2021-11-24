<template>
  <div>
    <li>
      <div :class="{done: checkbox}">
        <strong>{{items.id}}</strong>
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
      id: ''
    }
  },
  props: ['items'],
  methods: {
    removeTodo(id) {
      eventBus.$emit('remTodo', this.item)
    }
  }
}
</script>

<style scoped>
li{
  display: flex;
  align-items: center;
  border: 1px solid rgba(199, 194, 194, 0.78);
  padding: 8px;
  margin-bottom: 18px;
  border-radius: 5px;
  box-shadow: 1px 5px 7px #dfdfdf;
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