<template>
  <div class="container">
    <CurrentDate v-bind:country="country"></CurrentDate>
    <div class="main">
      <MainInformation
        title="Cases"
        v-bind:count="totalNewCases"
        class="main-child"
      ></MainInformation>
      <MainInformation
        title="Deaths"
        v-bind:count="totalDeathCases"
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
  mounted() {
    // loads when vue attaches the component to the html dom
    // mounted lifecycle hook
    fetch(`https://api.covid19api.com/summary`)
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.country = data.Country;
      })
      .catch(() => {
        this.showError = true;
      });
  },

  methods: {
    resetCountry() {
      this.totalNewCases = 0;
      this.totalDeathCases = 0;
      this.country = "";
    },
    closePopup() {
      this.showPopup = false; //we close the popup by setting showPopup to false
      this.showError = false;
    },
    onSelectedCountry(country) {
      //here we can save the selected country in the localstorage
      this.totalNewCases = 0;
      this.totalDeathCases = 0;
      this.country = country;

      if (this.country !== "") {
        this.countryObject = this.countries.find((object) => {
          //returns boolean
          return object.Country.toLowerCase() === this.country.toLowerCase();
        });
      }

      if (this.countryObject) {
        this.totalNewCases = this.countryObject.TotalConfirmed;
        this.totalDeathCases = this.countryObject.TotalDeaths;
      } else {
        //pop up n/a
        this.totalNewCases = "n/a";
        this.totalDeathCases = "n/a";
        this.showPopup = true;
      }
    },
  },
  data: function () {
    return {
      countryObject: {},
      countries: [],
      country: "",
      totalNewCases: 0,
      totalDeathCases: 0,
      showPopup: false,
      showError: false,
    };
  },
};
</script>

<style>
.container {
  max-width: 1100px;
  margin-left: auto;
  margin-right: auto;
}
.main {
  display: flex;
  justify-content: space-around;
}
.main-child {
  width: 45%;
}
@media only screen and (max-width: 767px) {
  .main {
    display: flex;
    flex-direction: column;
  }
  .main-child {
    width: 100%;
    margin-bottom: 1rem;
  }
}
</style>