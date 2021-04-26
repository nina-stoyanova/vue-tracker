<template>
  <header class="header">
    COVID 19 Tracker
    <h3 class="h3">API by covid19api.com</h3>
    <img class="icon" alt="icon" src="@/assets/icons/pause-solid.svg" />
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
  background-color: blue;
  color: white;
  padding: 2px;
}

.h3 {
  font-size: 0.5rem;
}
.icon {
  width: 1rem;
}
</style>
