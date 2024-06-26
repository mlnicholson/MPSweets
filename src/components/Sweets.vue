<template>
  <div>
    <div class="action-bar">
      <filterSelector
        label="Search Sweets"
        v-model="sweetListFilter"
        tooltip="Filter the data to show sweets that contain your search string. Case sensitive."
        @filterChanged="filterSweetList"
        :disabled="showSweetForm"
      >
      </filterSelector>
      <button class="button add" @click="openSweetForm" :disabled="showSweetForm">Add Sweet</button>
    </div>
    <sweetForm
      :showForm="showSweetForm"
      v-model="sweetItem"
      @cancel="closeForm"
      @add="addSweet($event)"
    >
    </sweetForm>
    <table>
      <tr>
        <th class="text-left sortable" style="min-width:50px;" @click="sortByColumn('id')" v-html="sortableColumnTitle('Id')"></th>
        <th class="text-left sortable" style="min-width:100px;" @click="sortByColumn('type')" v-html="sortableColumnTitle('Type')"></th>
        <th class="text-left" style="min-width:150px;">Name</th>
        <th class="text-left sortable" @click="sortByColumn('topping')" v-html="sortableColumnTitle('Topping')"></th>
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
import filterSelector from '@/components/FilterSelector.vue'
import sweetForm from '@/components/SweetForm.vue'
export default {
  name: 'SweetsComponent',
  components: {
    filterSelector,
    sweetForm
  },
  props: {
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
      Ascending: true,
      OverlayIsActive: false
    },
    showSweetForm: false,
    sweetItem: {
      id: null,
      type: null,
      name: null,
      topping: null
    }
  }),
  methods: {
    sortableColumnTitle(columnName) {
      // Build the title for sortable columns in the data table. This includes a tooltip to highlight the column
      // can be sorted
      let title = "<span class='tooltip' style='width:100%'>" + columnName;
      
      // If this column is currently being sorted then highlight this with an up or down carat character
      if (this.sort.Column === columnName.toLowerCase())
        title = title + (this.sort.Ascending === true ? " &#9650;" : " &#9660;");

      return title + "<span class='tooltiptext'>Toggle sort order</span></span>";
    },
    sortByColumn(columnName) {
      this.sort.Column === columnName ? this.sort.Ascending = !this.sort.Ascending : true;
      this.sort.Column = columnName;
      this.sortData();
    },
    filterSweetList() {
      // Reset to the base data set if no filter given
      if (!this.sweetListFilter) {
        this.sweetList = [...sweetListData];
      }
      else {
        // Set the local sweetList variable to reflect a filtered version of the sweetList data set.
        // This is important to ensure that clearing the filter will restore data previously filtered
        // including newly added records 
        this.sweetList = sweetListData.filter((i) => 
          (i.id && i.id.includes(this.sweetListFilter)) || 
          (i.type && i.type.includes(this.sweetListFilter)) ||
          (i.name && i.name.includes(this.sweetListFilter)) ||
          (i.topping && i.topping.includes(this.sweetListFilter))
        );
      }
      this.sortData();
    },
    sortData() {
      //Sort the data in sweetlist based on the currently selected sort column and sort direction
      const direction = this.sort.Ascending ? 1 : -1;
      this.sweetList.sort((a, b) => (a[this.sort.Column] > b[this.sort.Column] ? direction : direction * -1));
    },
    openSweetForm() {
      this.showSweetForm = true;
    },
    closeForm() {
      this.showSweetForm = false;
    },
    addSweet(newSweet) {
      this.saveData(newSweet)
        .then(() => {
          // Once save is complete refresh the data table.
          // NB: I am assuming if a filter is present then the new record will be subject to
          // those filter rules so it may or may not appear in the list
          this.filterSweetList();
          this.showSweetForm = false;
        })
    },
    async saveData(newSweet) {
      // Save the new sweet to the base data set of sweets
      sweetListData.push({...newSweet});
    }
  },
  mounted() {
    // Import the sweetList data from file and copy to a local variable.
    // NB: It is important to copy the original data to ensure changes made
    // during the filtering process above do not affect the base data set
    this.sweetList = [...sweetListData];
    this.sortData();
  }
}
</script>

<style scoped>
/* Tables */
.text-left {
  text-align: left;
}
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
table {
  width: 100%;
  box-shadow: 0 5px 12px rgba(32,32,32,.3)
}
th {
  background-color: grey;
  color:white
}
th.sortable {
  cursor: pointer;
}
td {
  color: black;
}
th,td {
  padding: 10px 15px
}
tr:nth-child(odd) {
  background-color: #eeeeee;
}
tr:nth-child(even) {
  background-color: #faf9f9;
}

/* buttons */
.button.add {
  color: white;
  background: blue;
  margin: 2px 0 0 10px;
}

.action-bar {
  display: inline-flex;
}
</style>
