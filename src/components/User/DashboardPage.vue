<script lang="ts" setup>

// import AttendanceTime from "../User/DashboardPage/AttendanceTime.vue";
import { ref } from "vue";
import axios from "axios";
import Swal from "sweetalert2";

const uuidRegExPattern = /^[0-9a-fA-F]{8}\b-[0-9a-fA-F]{4}\b-[0-9a-fA-F]{4}\b-[0-9a-fA-F]{4}\b-[0-9a-fA-F]{12}$/gi;

const invalidQrId = ref(false);
const userId = ref(""); // User's UUID

const user = JSON.parse(localStorage.getItem('user') || '{}')

function timeIn() {
  axios.post(`/time/in/${user.id}`).then((res) => {
    if (res.status === 200) {
      Swal.fire({
        icon: "success",
        title: "Success!",
        text: "You timed in successfully. Don't forget to time out!",
        timer: 1500,
        showCancelButton: false,
        showConfirmButton: false
      });
      return;
    }
    if (res.status === 202) {
      axios.post(`/time/out/${user.id}`).then((res) => {
        if (res.status === 200) {
          Swal.fire({
            icon: "success",
            title: "Success!",
            text: "You timed out successfully.",
            timer: 1500,
            showCancelButton: false,
            showConfirmButton: false
          });
        }
      });
      return;
    }
  });
}

function timeOut() {
  if (!userId.value.match(uuidRegExPattern)) {
    invalidQrId.value = true;
    setTimeout(() => {
      invalidQrId.value = false;
    }, 3000);
    return;
  }

  axios.post(`/time/out/${userId.value}`).then((res) => {
    if (res.status === 200) {
      Swal.fire({
        icon: "success",
        title: "Success!",
        text: "You timed out successfully.",
        timer: 1500,
        showCancelButton: false,
        showConfirmButton: false
      });
    }
  });
}
</script>
<template>
 <div class="absolute w-1/5 mx-auto bottom-10 right-5">
  <AttendanceTime />
</div>
  <main>
    <div class="flex items-center justify-center w-full h-full mx-auto">
      <div :class="{ shake: invalidQrId }" class="p-10 bg-white shadow-2xl rounded-xl">
        <h1 class="p-4 text-3xl font-semibold text-center">Attendance Here</h1>
        <button v-if="!invalidQrId" @click="timeIn" class="w-40 p-4 mx-auto mt-4 text-lg font-semibold text-white bg-blue-500 rounded-lg">Time In</button>
        <button v-else @click="timeOut" class="w-40 p-4 mx-auto mt-4 text-lg font-semibold text-white bg-red-500 rounded-lg">Time Out</button>

      </div>
    </div>
  </main>
  

  
 
</template>

<style scoped>

.shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
}

@keyframes shake {

  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}
</style>
