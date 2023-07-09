<script lang="ts" setup>
import { ref } from "vue";
import moment from "moment";
moment.updateLocale(moment.locale(), { invalidDate: "No Data" });
const props = defineProps(["attendance"]);

const late = ref(false);
</script>
<template>
  <tr
    class="bg-white border-b"
  >
    <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
      {{ props.attendance.user.profile.lastName }}
      {{ props.attendance.user.profile.firstName }}
      {{ props.attendance.user.profile.middleName.charAt(0) }}.{{
        props.attendance.user.profile.suffix
      }}
    </th>

    <td class="px-6 py-4">
      {{ moment(props.attendance.recordDate).format("YYYY MMMM DD") }}
    </td>
    <td class="px-6 py-4">
      {{ moment(props.attendance.timeIn).format("hh:mm A") }}
    </td>
    <td class="px-6 py-4">
      {{ moment(props.attendance.timeOut).format("hh:mm A") }}
    </td>
   
    <!-- <td class="px-6 py-4 text-right">
            <a href="#" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</a>
          </td> -->
  </tr>
</template>
