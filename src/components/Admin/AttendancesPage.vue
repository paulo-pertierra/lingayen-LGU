<script lang="ts" setup>
import { ref } from "vue";
import AttendancesTableHead from "./AttendancesPage/AttendancesTableHead.vue";
import AttendancesTableEntry from "./AttendancesPage/AttendancesTableEntry.vue";
import axios from "axios";

const attendances = ref([]);
axios.get("/time").then((res) => {
  attendances.value = res.data;
});
</script>
<template>
  <p class="my-5 text-3xl text-black">Attendances</p>
  

  <div class="relative overflow-auto shadow-md ">
    <table class="w-full text-sm text-left text-black border ">
      <AttendancesTableHead />
      <tbody>
        <AttendancesTableEntry
          v-for="(attendance, index) in attendances"
          :key="index"
          :attendance="attendance"
        />
      </tbody>
    </table>
  </div>
</template>
