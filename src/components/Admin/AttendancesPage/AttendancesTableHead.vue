<script lang="ts" setup>
const tableHeads = ["NAME", "DATE", "TIME IN", "TIME OUT"];
</script>

<template>
  <thead
    class="sticky top-0 text-xs text-black uppercase bg-white border"
  >
    <tr class="border">
      <th v-for="(tableHead, index) in tableHeads" :key="index" scope="col" class="px-6 py-3">
        {{ tableHead }}
      </th>
    </tr>
  </thead>
</template>
