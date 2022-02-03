<template>
  <div class="container">
    <h1>TODO LIST</h1>
    <TodoList/>
  </div>


</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style lang="scss">
@import '@/assets/scss/style.scss';

h1{
  text-align: center;
  margin: 30px 0;
}


</style>
