<script setup>
import {ref} from 'vue'

const add_input = ref('');
const todos = ref([
]);

function doAdd() {
//  input_message.value = input_message.value.split('').reverse().join('')
  var input_data = add_input.value;

  if (input_data === '') {
    return;
  }
  todos.value.push({comment: input_data});
  add_input.value = '';
}

function doDelete(idx) {
  todos.value.splice(idx, 1);
}
</script>

<template>
  <div>
    <input type="text" v-model="add_input">
    <button v-on:click="doAdd">추가</button>
  </div>

  <div>
    <ol>
      <li class="todo_list" v-for="(value, index) in todos" :key="index">
        {{ value.comment }}
        <button v-on:click="doDelete(index)">완료</button>
      </li>
    </ol>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
