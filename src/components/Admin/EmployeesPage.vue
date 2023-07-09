<script lang="ts" setup>
import TableHead from "./EmployeesPage/EmployeeTableHead.vue";
import TableEntry from "./EmployeesPage/EmployeeTableEntry.vue";
import axios from "axios";
import { onMounted, ref, watch } from "vue";
import { initFlowbite } from "flowbite";

import { library } from "@fortawesome/fontawesome-svg-core";
import { faUserPlus } from "@fortawesome/free-solid-svg-icons";
library.add(faUserPlus);

import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

import { useEmployeeTableSorterStore } from "@/stores/pinia";

const sort = useEmployeeTableSorterStore();
const employees = ref([]);

onMounted(() => {
  axios.get(`/users?profile=true`).then((res) => {
    employees.value = res.data;
  });
});

watch(sort, () => {
  axios.get(`/users?profile=true&sort=${sort.order}&sortBy=${sort.by}`).then((res) => {
    employees.value = res.data;
  });
});

onMounted(() => initFlowbite());
</script>

<template>
  <p class="my-6 mt-5 text-3xl text-black">Employees</p>
  <div class="flex justify-between">


  </div>
  <div class="relative overflow-x-auto shadow-md max-h-144">
    <table class="w-full overflow-auto text-sm text-left text-black border ">
      <TableHead />
      <tbody>
        <TableEntry v-for="(employee, index) in employees" :key="index" :info="employee" />
      </tbody>
    </table>
  </div>
</template>
