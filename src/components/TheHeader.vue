<template>
  <header class="header">
    <div class="container">
      <img
        class="icons-container__big"
        alt="icon"
        src="@/assets/icons/virus.svg"
      />
      <img
        class="icons-container__small"
        alt="icon"
        src="@/assets/icons/virus.svg"
      />
      COVID 19 Tracker
    </div>
    <!-- <h3 class="url">API by covid19api.com</h3> -->
    <span class="url">API by </span>
    <span class="url-blue">covid19api.com</span>
  </header>
</template>

<script>
export default {
  name: "TheHeader",
  props: {},
};
</script>

<style>
.header {
  background-color: #4233b4;
  color: white;
  padding: 2px;
}

.url {
  font-size: 0.5rem;
}
.url-blue {
  color: lightblue;
  font-size: 0.5rem;
}
.icons-container__big {
  width: 1rem;
  background-color: white;
  padding: 1px;
  margin: 5px 2px 0 0;
}
.icons-container__small {
  width: 0.6rem;
  background-color: white;
}
</style>
