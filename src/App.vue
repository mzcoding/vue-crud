<template>
  <div id="app">
    <h2>Список сотрудников</h2><br>
    <Staff/>
  </div>
</template>

<script>
import Staff from './components/Staff.vue'

export default {
  name: 'App',
  components: {
    Staff
  }
}
</script>

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
