<template>
  <div>
    <label for="filter">{{label}}: </label>
    <input class="filter" id="filter" v-model="inputVal" @keyup="applyFilter" :disabled="disabled">
    <h2 class="tooltip">&#9432;
      <span class="tooltiptext">{{tooltip}}</span>
    </h2>
  </div>
</template>

<script>
export default {
  name: 'FilterComponent',
  props: {
    label: null,
    value: null,
    tooltip: null,
    disabled: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    inputVal: {
      get() {
        return this.value;
      },
      set(val) {
        this.$emit('input', val);
      }
    }
  },
  methods: {
    applyFilter() {
      this.$emit("filterChanged");
    }
  }
}
</script>

<style scoped>
.filter {
  margin-bottom: 5px;
  margin-left: 5px;
  margin-right: 5px;
}

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
  margin-left: -100px;

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
