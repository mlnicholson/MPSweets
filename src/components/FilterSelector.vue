<template>
  <div>
    <label for="filter">{{label}}: </label>
    <input class="filter" id="filter" v-model="inputVal" @keyup="applyFilter">
    <div class="tooltip">&#9432;
      <span class="tooltiptext">{{tooltip}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FilterComponent',
  props: {
    label: null,
    value: null,
    tooltip: null
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
  border-bottom: 1px dotted black; /* If you want dots under the hoverable text */
}

/* Tooltip text */
.tooltip .tooltiptext {
  visibility: hidden;
  width: 200px;
  background-color: #555;
  color: #fff;
  text-align: center;
  padding: 5px 0;
  border-radius: 6px;

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
