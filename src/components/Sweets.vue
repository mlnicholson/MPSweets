<template>
  <div>
    <h1>{{ title }}</h1>
    
    <sortSelector
      label="Sort By"
      :columnList="sort.ColumnList"
      v-model="sort.Column"
      @sortColumnChanged="sortData"
      @sortOrderChanged="sortOrderChanged($event)"
    ></sortSelector>
    <table class="center">
      <tr>
        <th class="text-left" style="width:50px;">Id</th>
        <th class="text-left" style="width:100px;">Type</th>
        <th class="text-left" style="width:150px;">Name</th>
        <th class="text-left">Topping</th>
      </tr>
      <tr
        v-for="(item, index) in sweetList"
        :key="index">
        <td class="text-left">{{ item.id }}</td>
        <td class="text-left">{{ item.type }}</td>
        <td class="text-left">{{ item.name }}</td>
        <td class="text-left">{{ item.topping }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import sweetList from "@/data/sweets.json";
import sortSelector from '@/components/SortSelector.vue'
export default {
  name: 'SweetsComponent',
  components: {
    sortSelector
  },
  props: {
    title: String
  },
  data: () => ({
    sweetList: [],
    sort: {
      ColumnList: [
        {"Value": "id", "Text": "Id"},
        {"Value": "type", "Text": "Type"},
        {"Value": "topping", "Text": "Topping"}
      ],
      Column: "id",
      Ascending: true
    },
  }),
  methods: {
    sortOrderChanged(isAscendingOrder) {
      this.sort.Ascending = isAscendingOrder;
      this.sortData();
    },
    sortColumnChanged() {
      this.sortData();
    },
    sortData() {
      //Sort the data in sweetlist based on the currently selected sort column and sort direction
      const direction = this.sort.Ascending ? 1 : -1;
      this.sweetList.sort((a, b) => (a[this.sort.Column] > b[this.sort.Column] ? direction : direction * -1));
    }
  },
  mounted() {
    // Import the sweetList data from file
    this.sweetList = sweetList;
  }
}
</script>

<style scoped>
.text-left {
  text-align: left;
}
.center {
  margin-left: auto;
  margin-right: auto;
}
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}

h3 {
  margin: 40px 0 0;
}
</style>
