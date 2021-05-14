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
  transition: all 500ms;
  position: fixed;
  left: 50%;
  top: 45%;
  width: 300px;
  padding: 2rem;
  background-color: white;
  color: rgb(209, 56, 56);
  box-shadow: 2px 2px 2px 2px #ccc;
  border: 2px solid black;
  border-radius: 12px;
  transform: translate(-50%, -300px);
}
.visible {
  opacity: 1;
  transform: translate(-50%, 0);
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
@media only screen and (max-width: 767px) {
}
</style>