<div class="back"></div>
<template>
 <div class="Apps" id="app">
 <todo-app></todo-app>
 </div>
 
</template>

<script>
import TodoApp from './components/TodoApp.vue'

export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>


