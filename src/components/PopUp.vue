<template>
  <div v-if="show" class="backdrop">
    <div class="popup-container">
      {{ message }}
      <button @click="onClose" class="popup-container__btn">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PopUp",
  props: ["show", "message"], //this is comming from outside?
  emits: ["popupClose"], //we declare the event with this name
  methods: {
    onClose() {
      this.$emit("popupClose");
    },
  },
};
</script>

<style>
.backdrop {
  position: fixed;
  background-color: rgba(211, 211, 211, 0.5);
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}
.popup-container {
  background-color: gray;
  position: fixed;
  left: 38%;
  top: 45%;
  padding: 2rem;
  color: white;
}
.popup-container__btn {
  position: absolute;
  top: 5px;
  right: 5px;
}
</style>