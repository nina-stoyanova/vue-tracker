<template>
  <div v-if="show" class="backdrop">
    <div class="popup-container">
      <img
        class="exclamation-mark"
        alt="warning"
        src="@/assets/icons/warning.svg"
      />
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
  background-color: white;
  position: fixed;
  left: 38%;
  top: 45%;
  padding: 2rem;
  color: rgb(209, 56, 56);
  box-shadow: 2px 2px 2px 2px #ccc;
  border: 2px solid black;
  border-radius: 12px;
}
.popup-container__btn {
  position: absolute;
  top: 5px;
  right: 5px;
  border-radius: 12px;
  background-color: rgb(209, 56, 56);
  color: white;
  border: 1px solid black;
}
.exclamation-mark {
  width: 2rem;
  position: absolute;
  top: 2px;
  right: 48%;
}
</style>