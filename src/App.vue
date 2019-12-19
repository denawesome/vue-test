<template>
  <div id="app">
    <Header />
    <div class="container py-5">
      <div class="row">
        <TodosList />
      </div>
    </div>
  </div>
</template>

<script>
import Header from '@/views/Header'
import TodosList from '@/components/TodosList.vue'

export default {
  components: {
    Header, TodosList
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
