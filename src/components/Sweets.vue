<template>
  <div>
    <h1>{{ title }}</h1>
    <filterSelector
      label="Search Sweets"
      v-model="sweetListFilter"
      @filterChanged="filterSweetList"
    >
    </filterSelector>
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
import sweetListData from "@/data/sweets.json";
import sortSelector from '@/components/SortSelector.vue'
import filterSelector from '@/components/FilterSelector.vue'
export default {
  name: 'SweetsComponent',
  components: {
    sortSelector,
    filterSelector
  },
  props: {
    title: String
  },
  data: () => ({
    sweetList: [],
    sweetListFilter: null,
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
    filterSweetList() {
      // Set the local sweetList variable to reflect a filtered version of the sweetList data set.
      // This is important to ensure that clearing the filter will restore data previously filtered
      // including newly added records 
      this.sweetList = sweetListData.filter((i) => 
        i.id.includes(this.sweetListFilter) || 
        i.type.includes(this.sweetListFilter) ||
        i.name.includes(this.sweetListFilter) ||
        i.topping.includes(this.sweetListFilter)
      );
      this.sortData();
    },
    sortData() {
      //Sort the data in sweetlist based on the currently selected sort column and sort direction
      const direction = this.sort.Ascending ? 1 : -1;
      this.sweetList.sort((a, b) => (a[this.sort.Column] > b[this.sort.Column] ? direction : direction * -1));
    }
  },
  mounted() {
    // Import the sweetList data from file and copy to a local variable.
    // NB: It is important to copy the original data to ensure changes made
    // during the filtering process above do not affect the base data set
    this.sweetList = [...sweetListData];
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
