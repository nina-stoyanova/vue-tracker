<template>
  <select @change="onChange" name="countries" id="count">
    <option v-for="country in countries" :key="country" v-bind:value="country">
      {{ country }}
    </option>
  </select>
  <div class="button">
    <button @click="onClick" type="button" class="btn">Clear country</button>
  </div>
</template>

<script>
import { countryList } from "../data/countries.js";

export default {
  name: "DropDown",
  data: function () {
    return {
      countries: countryList,
      selectedCountry: "",
    };
  },
  mounted() {
    //console.log(countryList);
  },
  methods: {
    onChange(eventInfo) {
      this.selectedCountry = eventInfo.target.value;
      //raise event
      this.$emit("selectedCountry", this.selectedCountry);
    },
    onClick() {
      this.selectedCountry = "";
      this.$emit("selectedCountry", this.selectedCountry);
    },
  },
};
</script>


<style>
</style>