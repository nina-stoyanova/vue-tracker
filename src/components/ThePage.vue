<template>
  <div>
    <CurrentDate v-bind:country="country"></CurrentDate>
    <div class="main">
      <MainInformation
        title="Cases"
        v-bind:count="casesCount"
        class="main-child"
      ></MainInformation>
      <MainInformation
        title="Deaths"
        v-bind:count="deathsCount"
        class="main-child"
        isDeaths="true"
      ></MainInformation>
    </div>
    <DropDown
      @selectedCountry="onSelectedCountry"
      @resetCountry="resetCountry"
    ></DropDown>
    <PopUp
      v-bind:show="showPopup"
      @popupClose="closePopup"
      message="No data available for this country"
    ></PopUp>
    <PopUp
      v-bind:show="showError"
      @popupClose="closePopup"
      message="Server is down"
    ></PopUp>
    <!-- v-bind - in order to accept it as varaible, not string -->
  </div>
</template>

<script>
import CurrentDate from "./CurrentDate.vue";
import MainInformation from "./MainInformation.vue";
import PopUp from "./PopUp.vue";
import DropDown from "./DropDown.vue";

export default {
  name: "ThePage",
  props: {},
  components: {
    CurrentDate,
    MainInformation,
    DropDown,
    PopUp,
  },

  methods: {
    resetCountry() {
      this.casesCount = 0;
      this.deathsCount = 0;
      this.country = "";
    },
    closePopup() {
      this.showPopup = false; //we close the popup by setting showPopup to false
      this.showError = false;
    },
    onSelectedCountry(country) {
      //here we can save the selected country in the localstorage
      this.casesCount = 0;
      this.deathsCount = 0;
      this.country = country;
      //if country is empty don't do the fetch
      if (this.country !== "") {
        fetch(
          `https://api.covid19api.com/country/${country}/status/confirmed?from=2020-03-01T08:00:00Z&to=2020-03-01T09:00:00Z`
        )
          .then((response) => {
            return response.json(); //decodding the response for js
          })
          .then((data) => {
            if (data.length === 0) {
              this.casesCount = "n/a";
              this.showPopup = true;
            } else {
              this.casesCount = data[0].Cases;
              console.log(this.country, this.casesCount);
            }
          })
          .catch((error) => {
            console.log(error);
            this.showError = true;
          });

        fetch(
          `https://api.covid19api.com/country/${country}/status/deaths?from=2020-03-01T08:00:00Z&to=2020-03-01T09:00:00Z`
        )
          .then((response) => {
            return response.json();
          })
          .then((answer) => {
            if (answer.length === 0) {
              this.deathsCount = "n/a";
              this.showPopup = true;
            } else {
              this.deathsCount = answer[0].Cases;
              console.log(this.country, this.deathsCount);
            }
          })
          .catch((error) => {
            console.log(error);
            this.showError = true; //we change this in 10places?
          });
      }
    },
  },
  data: function () {
    return {
      country: "",
      casesCount: 0,
      deathsCount: 0,
      showPopup: false,
      showError: false,
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