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

  //   mounted() {
  //     //this.getPromise().then(result => console.log(result));
  //     fetch("https://www.boredapi.com/api/activity")
  //       .then((httpResponse) => {
  //         return httpResponse.json();
  //       })
  //       .then((body) => {
  //         console.log(body);
  //         this.activity = body;
  //       })
  //       .catch((error) => {
  //         console.log(error);
  //         //create a popup
  //       });
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
