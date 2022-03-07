<script setup>
import {ref, computed} from 'vue'

const add_input = ref('');
const todos = ref([
]);

// const fullName = computed({
//   get: () => `${lastName.value} ${firstName.value}`.trim(),
//   set: (newValue) => {
//     const names = newValue.trim().split(' ');
//     lastName.value = names[0] ?? '';
//     firstName.value = names[1] ?? '';
//   }
// });
let cntAll = ref(0);
const computedAllCnt = computed({
  get: () => todos.value,
  set: (newValue) => {
    return newValue.filter((element) => {
      return element
    })
  }
});

function doAdd() {
//  input_message.value = input_message.value.split('').reverse().join('')
  var input_data = add_input.value;

  if (input_data === '') {
    return;
  }
  todos.value.push({comment: input_data, status: false});
  add_input.value = '';
}

function doDelete(idx) {
  todos.value.splice(idx, 1);
}

function doDone(idx) {
  todos.value[idx].status = !todos.value[idx].status;
}
</script>

<template>
  <div>
    <form @submit.prevent="doAdd">
      <input type="text" v-model="add_input" autofocus>
      <button>추가</button>
    </form>
  </div>

  <div>
    <ol>
      <li v-for="(value, index) in todos" :key="index">
        <div>
          <input type="checkbox" @click="doDone(index)" v-model="value.status">
          <label :class="{done: value.status === true}">{{ value.comment }}</label>
          <button v-on:click="doDelete(index)">완료</button>
        </div>
      </li>
    </ol>
  </div>
  <div>
    <span>All: </span><span>{{ computedAllCnt.length }}</span>
    <span>Todo: </span><span></span>
    <span>Done: </span><span></span>
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

.done {
  text-decoration: line-through;
  color: gray;
}
</style>
