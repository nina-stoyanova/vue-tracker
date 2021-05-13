<template>
  <div :class="{ hidden: true, visible: show }">
    <img
      class="exclamation-mark"
      alt="warning"
      src="@/assets/icons/warning.svg"
    />
    {{ message }}
    <button @click="onClose" class="popup-container__btn">Close</button>
  </div>
</template>

<script>
export default {
  name: "PopUp",
  data() {
    return {
      active: false,
    };
  },
  props: ["show", "message"], //this is comming from outside?
  emits: ["popupClose"], //we declare the event with this name
  mounted() {},
  methods: {
    changePopUp() {
      setTimeout(() => {
        this.active = true; //activate the box
      }, 3000);
    },
    onClose() {
      this.$emit("popupClose");
    },
  },
};
</script>

<style>
.hidden {
  opacity: 0;
  transform: translateY(-300px);
  background-color: blueviolet;
  transition: opacity 2s;
  transition: transform 2s;
}
.visible {
  opacity: 1;
  transform: translateY(0);
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