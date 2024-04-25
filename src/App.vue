<template>
  <div id="app">
    <div style="display: inline-flex; align-items: center;">
      <img alt="Sweets logo" src="./assets/donut.png" style="width: 160px">
      <h1>The Sweets App</h1>
    </div>
    <Sweets/>    
  </div>
</template>

<script>
import Sweets from '@/components/Sweets.vue'

export default {
  name: 'App',
  components: {
    Sweets
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 10px;
}
</style>