<script setup lang="ts">
  import { ref } from "vue";

  const tableData = ref([{
    "id": 1,
    "name": "name 1",
    "age": 5
  }, {
    "id": 2,
    "name": "name 2",
    "age": 10
  }, {
    "id": 3,
    "name": "name 3",
    "age": 15
  }, {
    "id": 4,
    "name": "name 4",
    "age": 20
  }, {
    "id": 5,
    "name": "name 5",
    "age": 25
  }
  ]);

  let currentPage = ref(1);

  // add pagination handlers for the buttons
  const handlePrevious = () => {
    console.log("Previous button clicked");
    currentPage.value--;
    if (currentPage.value < 1) {
      currentPage.value = 1;
    }

  };
 
  const handleNext = () => {
    console.log("Next button clicked");
    currentPage.value++;
    const maxPage = Math.ceil(tableData.value.length / 3);
    if (currentPage.value > maxPage) {
      currentPage.value = maxPage;
    }
  };
  
</script>

<template>
  <!-- add a table to display the tableData, but
    limit it to 3 items per page -->
  <table>
    <thead>
      <tr>
        <th>Id</th>
        <th>Name</th>
        <th>Age</th>
      </tr>
    </thead>
    <tbody>
      <!-- use the slice method to limit the tableData
        based on currentPage and to 3 items per page -->
      <tr v-for="item in tableData.slice((currentPage - 1) * 3, currentPage * 3)" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.age }}</td>
      </tr>
    </tbody>
  </table>
  <!-- add pagination buttons for the table -->
  <div>
    <button v-on:click="handlePrevious">Previous</button>
    <button v-on:click="handleNext">Next</button>
  </div>
</template>

<style scoped>

table {
  border-collapse: collapse;
  width: 100%;
  background: orange;
}
/* style the table header */
th {
  background-color: #4caf50;
  color: white;
}
/* style the table rows */
tr:nth-child(even) {
  background-color: #123456;
}
/* style the table data cells */
td {
  border: 1px solid #ddd;
}
</style>
