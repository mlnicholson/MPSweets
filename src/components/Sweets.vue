<template>
  <div>
    <h1>{{ title }}</h1>
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
export default {
  name: 'SweetsComponent',
  props: {
    title: String
  },
  data: () => ({
    sweetList: [],
  }),
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
