<template>
  <div>
    <CurrentDate v-bind:country="country"></CurrentDate>
    <div class="main">
      <MainInformation
        title="Cases"
        count=""
        total=""
        class="main-child"
      ></MainInformation>
      <MainInformation
        title="Deaths"
        count=""
        total=""
        class="main-child"
      ></MainInformation>
    </div>
    <DropDown @selectedCountry="onSelectedCountry"></DropDown>
  </div>
</template>

<script>
import CurrentDate from "./CurrentDate.vue";
import MainInformation from "./MainInformation.vue";

import DropDown from "./DropDown.vue";

export default {
  name: "ThePage",
  props: {},
  components: {
    CurrentDate,
    MainInformation,
    DropDown,
  },
  methods: {
    onSelectedCountry(country) {
      this.country = country;
    },
  },
  data: function () {
    return {
      country: "",
    };
  },
};
</script>

<style>
.main {
  display: flex;
}
.main-child {
  width: 50%;
}
</style>