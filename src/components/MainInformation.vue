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
  margin-right: 30px;
  margin-left: 30px;
}
.covid-stats--deaths {
  background-color: #9bc7ff;
  margin-right: 30px;
  margin-left: 30px;
}
.covid-stats__title {
  font-weight: bold;
  color: blue;
  font-size: 1.5rem;
}
/* DO THE STYLES FOR THE REST */
</style>