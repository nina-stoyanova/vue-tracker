<template>
  <select @change="onChange" name="countries" id="count" class="drop-down">
    <!-- v-model - connection between the chosen country and the property
    selectedCountry -->
    <option
      v-for="country in countries"
      :key="country"
      v-bind:value="country.Slug"
    >
      {{ country.Country }}
    </option>
  </select>

  <div class="reset-container">
    <button @click="onReset" type="button" class="reset-container-btn">
      Clear country
    </button>
  </div>
</template>

<script>
export default {
  name: "DropDown",
  emits: ["selectedCountry", "resetCountry"],
  data: function () {
    return {
      countries: [],
      //selectedCountry: "",
    };
  },

  mounted() {
    //executes only one time when is loaded
    const userChoice = window.localStorage.getItem("selectedCountry");
    if (userChoice) {
      //this means if userChoice is something meaningfull
      //this.selectedCountry = userChoice;
    }
    this.getCountries();
  },
  methods: {
    onChange(eventInfo) {
      //here we can save the selected country in localstorage
      let selectedCountry = eventInfo.target.value;
      window.localStorage.setItem("selectedCountry", selectedCountry);
      this.$emit("selectedCountry", selectedCountry);
    },
    onReset() {
      //this.selectedCountry = "";
      this.$emit("resetCountry");
    },
    getCountries() {
      fetch("https://api.covid19api.com/countries")
        .then((response) => {
          return response.json();
        })
        .then((result) => {
          let sortedCountries = result.sort((a, b) => {
            //if we want a to be before b, than return negative number
            let firstObjectCountryName = a.Country; //Germany
            let secondObjectCountryName = b.Country; //France
            if (firstObjectCountryName < secondObjectCountryName) {
              //if first < second
              //we want a to be before b
              return -8;
            } else {
              return 8;
            }
          });
          this.countries = sortedCountries;
        });
    },
  },
};
</script>


<style>
.drop-down {
  margin-top: 20px;
  width: 95%;
  font-size: 1rem;
}
.reset-container {
  position: relative;
}
.reset-container-btn {
  position: absolute;
  left: 5px;
  margin-top: 20px;
  background-color: #2b7037;
  color: white;
  font-size: 0.8rem;
}
/* style hoover btn border box shadow */
</style>