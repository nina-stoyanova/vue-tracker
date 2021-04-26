<template>
  <div>{{ currentDate }}</div>
</template>

<script>
export default {
  name: "CurrentDate",
  props: [],
  data: function () {
    return {
      currentDate: "",
    };
  },
  created() {
    setInterval(this.getNow, 1000);
  },

  methods: {
    getNow: function () {
      const today = new Date();
      const date =
        today.getFullYear() +
        "-" +
        (today.getMonth() + 1) +
        "-" +
        today.getDate();
      const time =
        today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
      const dateTime = date + " " + time;
      this.currentDate = dateTime;
    },
  },
};
</script>

<style>
</style>