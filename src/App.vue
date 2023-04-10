<template>
  <div id="app">
    <TodoAddVue/>
    <!-- <todo-app></todo-app> -->
  </div>
</template>

<script>
import TodoAddVue from './components/TodoAdd.vue'
// import TodoApp from './components/TodoApp.vue'

export default {
  name: 'App',
  components: {
    // TodoApp,
    TodoAddVue
  }
}
</script>