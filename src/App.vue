<template>
  <div id="app">
    <HeaderHome></HeaderHome>
    <TodoTask></TodoTask>
  </div>
</template>

<script>
import HeaderHome from './components/HeaderHome.vue';
import TodoTask from './components/TodoTask.vue';

export default {
  name: 'App',
  components: {
    HeaderHome,
    TodoTask,
  }
}
</script>

<style>

</style>