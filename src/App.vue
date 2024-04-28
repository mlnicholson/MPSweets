<template>
  <div id="app">
    <div class="main">
      <div style="display: inline-flex; align-items: center;">
        <img alt="Sweets logo" src="./assets/donut.png" style="width: 160px">
        <h1>The Sweets App</h1>
      </div>
      <Sweets/>  
    </div>  
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
body {
  font-size:16px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: aliceblue;
}
.main {
  margin: 10px;
  min-height: 97vh;
}

/* Global Styles */
input {
  padding: 10px 15px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  border-radius: 5px;
  border-width: 1px;
  font-size:inherit;
}
input:disabled {
  cursor: not-allowed;
}

select {
  padding: 10px 15px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  border-radius: 5px;
  border-width: 1px;
  font-size:inherit;
}
select:disabled {
  cursor: not-allowed;
}

button {
  height: 35px;
  border-radius: 5px;
  border: none;
  font-weight: bold;
  font-size:inherit;
  cursor: pointer;
}
button:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

label {
  font-size:inherit;
  font-weight: bold;
}
</style>