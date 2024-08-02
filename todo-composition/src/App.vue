<script setup>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'
import { onMounted, ref } from 'vue'

const todoItems = ref([])
onMounted(() => {
  if (localStorage.length > 0) {
    for (let i = 0; i < localStorage.length; i++) {
      todoItems.value.push(localStorage.key(i))
    }
  }
})
const addTodo = (todoItem) => {
  localStorage.setItem(todoItem, todoItem)
  todoItems.value.push(todoItem)
}

const removeTodo = (todoItem, index) => {
  localStorage.removeItem(todoItem)
  todoItems.value.splice(index, 1)
}

const removeAll = () => {
  localStorage.clear()
  todoItems.value = []
}
</script>

<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-on:removeTodo="removeTodo" v-bind:propsdata="todoItems"></TodoList>
    <todo-footer v-on:removeAll="removeAll"></todo-footer>
  </div>
</template>

<style>
body {
  text-align: center;
  background: #f6f6f8;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
