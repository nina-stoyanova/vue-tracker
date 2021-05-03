<template>
  <div class="country">{{ country }}</div>
  <div class="date">{{ currentDate }}</div>
</template>

<script>
import moment from "moment";

export default {
  name: "CurrentDate",
  props: ["country"],
  data: function () {
    return {
      currentDate: "",
    };
  },
  created() {
    this.getNow();
    this.currentDate = this.getCurrentDateTime();
    //setInterval(this.getNow, 1000);
  },

  methods: {
    getCurrentDateTime() {
      return moment().format("MMMM Do YYYY HH:mm:ss"); //format string
    },
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
  color: black;
}
.country {
  font-weight: bold;
  text-transform: capitalize;
}
</style>