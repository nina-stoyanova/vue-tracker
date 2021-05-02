<template>
  <div>
    <CurrentDate v-bind:country="country"></CurrentDate>
    <div class="main">
      <MainInformation
        title="Cases"
        v-bind:count="casesCount"
        total=""
        class="main-child"
      ></MainInformation>
      <MainInformation
        title="Deaths"
        count=""
        total=""
        class="main-child"
        isDeaths="true"
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
      this.casesCount = 0;
      this.country = country;
      //if country is empty don't do the fetch
      if (this.country !== "") {
        fetch(
          `https://api.covid19api.com/country/${country}/status/deaths?from=2020-03-01T08:00:00Z&to=2020-03-01T09:00:00Z`
        )
          .then((response) => {
            return response.json();
          })
          .then((data) => {
            if (data.length === 0) {
              this.casesCount = "n/a";
            } else {
              this.casesCount = data[0].Cases;
              console.log(this.country, this.casesCount);
            }
          });
      }
    },
  },
  data: function () {
    return {
      country: "",
      casesCount: 0,
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