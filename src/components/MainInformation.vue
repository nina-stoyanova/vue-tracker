<template>
  <div class="box">
    <div class="information">{{ title }}</div>
    <div class="information">New: {{ count }}</div>
    <div class="information">Total: {{ total }}</div>
  </div>
</template>

<script>
export default {
  name: "MainInformation",
  props: ["title", "count", "total"],
};
</script>


<style>
</style>