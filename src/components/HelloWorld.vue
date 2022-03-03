<script setup>
import { ref } from 'vue'
import Todo from './Todo.vue'

defineProps({
  msg: String
})

const count = ref(0)
</script>

<template>

  <Todo>

  </Todo>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
