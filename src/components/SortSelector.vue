<template>
  <div>
    <label for="sort">{{label}}: </label>
    <select name="sort" id="sort" @change="sortColumnChanged($event)" v-model="inputVal">
      <option
        v-for="(item, index) in columnList"
        :key="index" 
        :value=item.Value>{{item.Text}}</option>
    </select>
    <div class="radioSet">
      <input type="radio" id="asc" name="sortOrder" @click="sortOrderChanged(true)" :checked="ascendingOrder">
      <label for="asc">Ascending</label>
      <input type="radio" id="desc" name="sortOrder" @click="sortOrderChanged(false)" :checked="!ascendingOrder">
      <label for="desc">Descending</label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SortSelectorComponent',
  props: {
    label: null,
    value: null,
    columnList: null,
    ascendingOrder: {
      type: Boolean,
      default: true
    }
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
    sortOrderChanged(ascendingSelected) {
      this.ascending = ascendingSelected;
      this.$emit("sortOrderChanged", ascendingSelected);
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
.radioSet {
  display: inline-flex;
  align-items: baseline;
  margin-bottom: 5px;
  margin-left: 5px;
}
</style>
