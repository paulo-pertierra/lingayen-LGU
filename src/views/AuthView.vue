<script lang="ts" setup>
import { RouterView } from "vue-router";
</script>

<template>
  <main>
    <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
      <div
        class="w-full bg-red-900 shadow-xl dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700"
      >
        <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
          <h1
            class="text-xl font-bold leading-tight tracking-tight text-center text-white md:text-2xl dark:text-white"
          >
            <a href="#" class="mx-auto text-2xl font-semibold text-gray-900 dark:text-white">
              <img class="w-20 h-20 mx-auto mb-10 sm:mb-5" src="../assets/lingayenlogo.png" alt="logo" />
            </a>
            Sign In
          </h1>
          <RouterView />
        </div>
      </div>
    </div>
  </main>
</template>

<style>
main {

    background-image: linear-gradient(to right, rgba(0, 0, 0, 0.85), rgba(0, 0, 0, 0.25)),url('../assets/capitol.jpg');
}
</style>
