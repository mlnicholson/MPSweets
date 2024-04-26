<template>
  <div>
    <label for="sort">{{label}}: </label>
    <select name="sort" id="sort" @change="sortColumnChanged($event)" v-model="inputVal">
      <option
        v-for="(item, index) in columnList"
        :key="index" 
        :value=item.Value>{{item.Text}}</option>
    </select>
    <button class="toggle sort" @click="sortOrderChanged">{{ ascending ? "Ascending" : "Descending"}}</button>
  </div>
</template>

<script>
export default {
  name: 'SortSelectorComponent',
  props: {
    label: null,
    value: null,
    columnList: null
  },
  data: () => ({
    ascending: true
  }),
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
    sortOrderChanged() {
      this.ascending = !this.ascending;
      this.$emit("sortOrderChanged", this.ascending);
    },
    sortColumnChanged() {
      this.$emit("sortColumnChanged");
    }
  }
}
</script>

<style scoped>
.sort {
  margin-bottom: 5px;
  margin-left: 5px;
  margin-right: 5px;
}
</style>
