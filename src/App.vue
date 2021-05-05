<template>
  <TheHeader></TheHeader>
  <ThePage></ThePage>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import ThePage from "./components/ThePage.vue";

export default {
  name: "App",
  components: {
    TheHeader,
    ThePage,
  },
  methods: {
    getPromise() {
      return new Promise((resolve) => setTimeout(() => resolve(42), 3000));
    },
  },
};
</script>

<style>
#app {
  font-family: "Quicksand", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
