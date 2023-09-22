<template>
  <div>
    <button @click="selectFile">Select CSV File</button>
    <div v-if="csvData.length > 0">
      <h2>CSV Data:</h2>
      <table>
        <thead>
          <tr>
            <th v-for="(header, index) in csvHeaders" :key="index">{{ header }}</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, rowIndex) in csvData" :key="rowIndex">
            <td v-for="(cell, cellIndex) in row" :key="cellIndex">
              <span v-if="!editingRow[rowIndex]">{{ cell }}</span>
              <input v-else v-model="editedRow[rowIndex][cellIndex]" />
            </td>
            <td>
              <button @click="editRow(rowIndex)">Edit</button>
              <button @click="deleteRow(rowIndex)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const csvData = ref([]);
const csvHeaders = ref([]);
const editingRow = ref([]);
const editedRow = ref([]);

const requiredHeaders = ['Name', 'Age', 'Country']; // Define your required headers here

const selectFile = () => {
  // Programmatically trigger the file input element
  const fileInput = document.createElement('input');
  fileInput.type = 'file';
  fileInput.accept = '.csv';
  fileInput.addEventListener('change', handleFileUpload);
  fileInput.click();
};

const handleFileUpload = (event) => {
  const file = event.target.files[0];

  if (!file) {
    return;
  }

  const reader = new FileReader();

  reader.onload = (e) => {
    const fileContent = e.target.result;

    // Split the CSV content into rows
    const rows = fileContent.split('\n');

    if (rows.length < 2) {
      alert('The CSV file is empty or invalid.');
      return;
    }

    // Extract headers (first row)
    const headers = rows[0].split(',');

    // Check if the file contains the required headers
    if (!requiredHeaders.every((header) => headers.includes(header))) {
      alert('The selected CSV file does not contain all required headers.');
      return;
    }

    // Parse and store data
    csvHeaders.value = headers;
    csvData.value = [];

    for (let i = 1; i < rows.length; i++) {
      const cells = rows[i].split(',');
      csvData.value.push(cells);
      editingRow.value.push(false);
      editedRow.value.push(cells.slice()); // Clone the row for editing
    }
  };

  reader.readAsText(file);
};

const editRow = (index) => {
  editingRow.value[index] = !editingRow.value[index];
};

const deleteRow = (index) => {
  csvData.value.splice(index, 1);
  editingRow.value.splice(index, 1);
  editedRow.value.splice(index, 1);
};

definePageMeta({
    layout:''
})
</script>

<style>
/* Add your styling here */
</style>
