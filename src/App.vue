<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/donut.png" style="width: 160px">
    <Sweets title="Sweets"/>
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
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>