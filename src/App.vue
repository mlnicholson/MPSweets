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
/* Global Styles */
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

/* --- input fields --- */
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

/* --- buttons --- */
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

/* --- labels --- */
label {
  font-size:inherit;
  font-weight: bold;
}

/* --- tooltips --- */

/* Tooltip container */
.tooltip {
  position: relative;
  display: inline-block;
  font-weight: bold;
  cursor: pointer;
  margin: 0;
}

/* Tooltip text */
.tooltip .tooltiptext {
  visibility: hidden;
  width: 200px;
  background-color: #555;
  color: #fff;
  text-align: center;
  padding: 5px;
  border-radius: 5px;
  font-size: 15px;

  /* Position the tooltip text */
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -90px;

  /* Fade in tooltip */
  opacity: 0;
  transition: opacity 0.3s;
}

/* Tooltip arrow */
.tooltip .tooltiptext::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
}

/* Show the tooltip text when you mouse over the tooltip container */
.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
}
</style>