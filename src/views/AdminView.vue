<script lang="ts" setup>
import { onMounted, ref } from "vue";
import { initFlowbite } from "flowbite";
import axios from "axios";
import router from "@/router";
import { RouterLink, RouterView } from "vue-router";
const user = JSON.parse(localStorage.getItem("user") || "{}");

const name = ref("");
const username = ref("");
const role = ref("");

axios
  .get(`/users/${user.id}?profile=true`)
  .then((res) => {
    name.value = res.data.profile.lastName + " " + res.data.profile.firstName;
    username.value = res.data.username;
    role.value = res.data.role;
    console.log(res);
  })
  .catch((error) => {
    console.log(error);
  });

// initialize components based on data attribute selectors
onMounted(() => {
  initFlowbite();
});

// Log Out
function logOut() {
  localStorage.removeItem("user");
  router.push("/");
}
</script>
<template>
  
<nav class="fixed w-full mx-auto bg-red-900 border-gray-200 dark:bg-red-900">
  <div class="flex flex-wrap items-center justify-between max-w-screen-xl p-4 mx-auto">
    <a href="https://flowbite.com/" class="flex items-center">
        <img src="../assets/lingayenlogo.png" class="h-10 mr-3" alt="lingayen-logo" />
        <span class="self-center text-2xl font-semibold text-white whitespace-nowrap dark:text-white">Lingayen, Pangasinan</span>
    </a>
    <button data-collapse-toggle="navbar-default" type="button" class="inline-flex items-center p-2 ml-3 text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-red-900 dark:focus:ring-gray-600" aria-controls="navbar-default" aria-expanded="false">
      <span class="sr-only">Open main menu</span>
      <svg class="w-6 h-6" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z" clip-rule="evenodd"></path></svg>
    </button>
    <div class="hidden w-full md:block md:w-auto" id="navbar-default">
      <ul class="flex flex-col p-4 mt-4 font-medium border border-gray-100 rounded-lg md:p-0 bg-gray-50 md:flex-row md:space-x-8 md:mt-0 md:border-0 md:bg-red-900 dark:bg-red-900 md:dark:bg-red-900 ">
        <li>
          <a href="/" class="block py-2 pl-3 pr-4 text-white rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-amber-500 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">Home</a>
        </li>
        <li>
          <a href="attendances" class="block py-2 pl-3 pr-4 text-white rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-amber-500 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">Attendances</a>
        </li>
        <li>
          <a href="employees" class="block py-2 pl-3 pr-4 text-white rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-amber-500 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">Employees</a>
        </li>
        <li>
          <a @click="logOut()" href='' class="block py-2 pl-3 pr-4 text-white rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-amber-500 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">Logout</a>
        </li>
      </ul>
    </div>
  </div>
</nav>



  <div class="h-screen p-4 bg-white">
    <div class="w-full mt-14">
      <RouterView />
    </div>
  </div>
  <!-- drawer init and toggle -->

  <!-- drawer component -->
  
</template>
