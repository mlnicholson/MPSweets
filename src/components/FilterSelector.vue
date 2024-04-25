<template>
  <div>
    <label for="filter">{{label}}: </label>
    <input class="filter" id="filter" v-model="inputVal" @keyup="applyFilter">
  </div>
</template>

<script>
export default {
  name: 'FilterComponent',
  props: {
    label: null,
    value: null
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
    },
    test() {
      console.log(this.inputVal);
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
</style>
