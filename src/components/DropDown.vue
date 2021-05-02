<template>
  <select
    v-model="selectedCountry"
    @change="onChange"
    name="countries"
    id="count"
  >
    <option
      v-for="country in countries"
      :key="country"
      v-bind:value="country.Slug"
    >
      {{ country.Country }}
    </option>
  </select>

  <div class="reset-container">
    <button @click="onClick" type="button" class="reset-container-btn">
      Clear country
    </button>
  </div>
</template>

<script>
export default {
  name: "DropDown",
  emits: ["selectedCountry"],
  data: function () {
    return {
      countries: [],
      selectedCountry: "",
    };
  },
  mounted() {
    this.getCountries();
  },
  methods: {
    onChange() {
      //raise event
      this.$emit("selectedCountry", this.selectedCountry);
    },
    onClick() {
      this.selectedCountry = "";
      this.$emit("selectedCountry", this.selectedCountry);
    },
    getCountries() {
      fetch("https://api.covid19api.com/countries")
        .then((response) => {
          return response.json();
        })
        .then((result) => {
          this.countries = result;
        });
    },
  },
};
</script>


<style>
/* style hoover btn border box shadow */
</style>