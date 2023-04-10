<template>
    <!--Add Employee-->
    <p class="h-4 text-center font-semibold">Employee Details</p>
    <CollectionAdd
      @addEmployeeData="addEmployeeData"
      :key="addRender"
    ></CollectionAdd>
  
    <!--Employeedata List-->
    <div>
      <collectionList
        :employerData="employerData"
        @employPrefillData="editData"
        @deleteDetails="deleteDetails"
      />
    </div>
    <!--Edit Employee-->
    <CollectionEdit
      :editEmployeeData="employeePrefill"
      @editEmployee="updateEdit"
      :openEditModal="openEditModal"
    ></CollectionEdit>
  </template>
  <script setup lang="ts">
  import { ref } from "vue";
  const show = ref(false);
  let employerData = ref([]);
  const openEditModal = ref(false);
  let addRender = ref(0);
  const employeePrefill = ref({});
  // Add Employee
  const addEmployeeData = (data: Object) => {
    const body = {
      body: JSON.stringify(data),
    };
    // Storing employee details in localstorage
    localStorage.setItem("employeeGetData", body);
     employerData.value.unshift(data);
    addRender.value++;
  };
  const updateEdit = (data: any) => {
    openEditModal.value = false;
  };
  // Prefilling in edit employee modal
  const editData = (data: object) => {
    openEditModal.value = true;
    employeePrefill.value = data;
    console.log("prefill data", employeePrefill);
  };
  // Delete Employee
  const deleteDetails = (data: any) => {
    employerData.value.splice(data, 1);
    localStorage.setItem("employeeGetData", JSON.stringify(employerData.value));
  };
  </script>
  