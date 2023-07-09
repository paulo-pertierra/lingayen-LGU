<template>

    <div class="grid grid-cols-2 gap-4 p-3">
      <div class="ml-auto text-5xl font-bold text-gray-600">{{ currentTime }}{{ amPm }}</div>
      <div class="mr-auto text-5xl font-bold text-gray-600">
        {{ currentDay }}

    </div>
  </div>
</template>

<script>
export default {
  data() {
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
