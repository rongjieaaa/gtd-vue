<template>
  <div>
    <ToDoList msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList.vue'

export default {
  name: 'App',
  components: {
    ToDoList
  }
}
</script>

<style>
</style>
