<template>
  <div v-bind:class="{ 'covid-stats--deaths': isDeaths }" class="covid-stats">
    <div class="covid-stats__title">{{ title }}</div>
    <div class="covid-stats__count">New: {{ count }}</div>
  </div>
</template>

<script>
export default {
  name: "MainInformation",
  props: ["title", "count", "isDeaths"],
};
</script>


<style>
.covid-stats {
  background-color: #cee4ff;
  box-shadow: 3px 3px 3px 3px #ccc;
  padding: 1rem;
}
.covid-stats--deaths {
  background-color: #9bc7ff;
}
.covid-stats__title {
  font-weight: lighter;
  color: blue;
  font-size: 1.5rem;
}
/* DO THE STYLES FOR THE REST */
</style>