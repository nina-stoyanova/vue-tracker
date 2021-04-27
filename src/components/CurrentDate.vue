<template>
  <div class="country">{{ country }}</div>
  <div class="date">{{ currentDate }}</div>
</template>

<script>
export default {
  name: "CurrentDate",
  props: ["country"],
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
* {
  border: 1px solid red;
}
.country,
.date {
  padding: 1rem;
}
</style>