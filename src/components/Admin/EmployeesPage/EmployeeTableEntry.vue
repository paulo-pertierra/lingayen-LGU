<script lang="ts" setup>
import { useUserStore } from "@/stores/pinia";
import ViewEmployeeAttendance from "./Modals/ViewEmployeeAttendance.vue";

import { library } from "@fortawesome/fontawesome-svg-core";
import { faEye, faUserPen, faTrash, faXmark } from "@fortawesome/free-solid-svg-icons";
library.add(faEye, faUserPen, faTrash, faXmark);

import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import DeleteEmployee from "./Modals/DeleteEmployee.vue";
import router from "@/router";

const props = defineProps(["info"]);
const user = useUserStore();
</script>
<template>
  <tr
    class="bg-white border-b "
  >
    <th class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
      <RouterLink :to="'/admin/employees/' + props.info.id">
        {{ props.info.profile.lastName }},
        {{ props.info.profile.firstName }}
        {{ props.info.profile.middleName.charAt(0) }}.
        {{ props.info.profile.suffix }}
      </RouterLink>
    </th>

    <td class="px-6 py-4">{{ props.info.profile.contactNumber }}</td>
    <td class="px-6 py-4">{{ props.info.profile.contactEmail }}</td>
    <td class="px-6 py-4">
  
    </td>
    
  </tr>

  <!-- Main modal -->
  <div
    :id="props.info.id"
    tabindex="-1"
    aria-hidden="true"
    class="fixed top-0 left-0 right-0 z-50 hidden w-full p-4 overflow-x-hidden overflow-y-auto md:inset-0 h-[calc(100%-1rem)] max-h-full"
  >
    <ViewEmployeeAttendance :user-id="props.info.id" />
  </div>

  <!-- Deletion confirmation modal-->
  <div
    :id="props.info.id + 'delete'"
    tabindex="-1"
    aria-hidden="true"
    class="fixed top-0 left-0 right-0 z-50 hidden w-full p-4 overflow-x-hidden overflow-y-auto md:inset-0 h-[calc(100%-1rem)] max-h-full"
  >
    <DeleteEmployee :id="props.info.id" />
  </div>
</template>
