<script setup>
import Modal from './common/Modal.vue'
import { ref } from 'vue'
const newTodoItem = ref('')
const showModal = ref(false)

const emits = defineEmits(['addTodo'])

const addTodo = () => {
  if (newTodoItem.value !== '') {
    const value = newTodoItem.value && newTodoItem.value.trim()
    emits('addTodo', value)
    clearInput()
  } else {
    showModal.value = !showModal.value
  }
}
const clearInput = () => {
  newTodoItem.value = ''
}
</script>

<template>
  <div class="inputBox shadow">
    <input
      type="text"
      v-model="newTodoItem"
      placeholder="Type what you have to do"
      @keyup.enter="addTodo"
    />
    <span class="addContainer" @click="addTodo">
      <i class="addBtn fa fa-plus" aria-hidden="true"></i>
    </span>

    <Modal v-if="showModal">
      <template v-slot:header>
        <h3>경고</h3>
      </template>
      <template v-slot:footer>
        <span @click="showModal = false">
          할일을 입력하세요.
          <i class="closeModalbtn fa fa-times" aria-hidden="true"></i>
        </span>
      </template>
    </Modal>
  </div>
</template>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: inline-block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>
