<script setup>
import {ref, computed} from 'vue'

const add_input = ref('');
const todos = ref([
]);
const computedDoneCnt = computed({
  get: () => todos.value.filter(item => item.status === true),
});

const computedLeftCnt = computed({
  get: () => todos.value.filter(item => item.status === false),
});

function doAdd() {
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
    <span>All: </span><span>{{ todos.length }}</span>
    <span>Todo: </span><span>{{ computedLeftCnt.length}}</span>
    <span>Done: </span><span>{{computedDoneCnt.length}}</span>
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
