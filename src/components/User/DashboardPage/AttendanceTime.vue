<template>
  <div
    class="w-full p-5 mx-auto bg-red-900 border border-gray-200 rounded-lg shadow"
  >
    <div class="flex flex-row">
      <div class="pr-5 ml-auto text-3xl font-bold text-white">{{ currentTime }}{{ amPm }}</div>
      <div class="mr-auto text-3xl font-bold text-white">{{ currentDay }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      currentDay: "",
      currentTime: "",
      amPm: ""
    };
  },
  mounted() {
    this.updateDateTime();
    this.timer = setInterval(() => {
      this.updateDateTime();
    }, 1000);
  },
  unmounted() {
    clearInterval(this.timer);
  },
  methods: {
    updateDateTime() {
      const now = new Date();
      const dateOptions = {
        weekday: "long"
      };
      const timeOptions = {
        hour: "numeric",
        minute: "numeric"
      };
      this.currentDay = now.toLocaleDateString("en-US", dateOptions);
      this.currentTime = now.toLocaleTimeString("en-US", timeOptions).slice(0, 5);
      this.amPm = now.toLocaleTimeString("en-US", { hour12: true }).slice(-2);
    }
  }
};
</script>
