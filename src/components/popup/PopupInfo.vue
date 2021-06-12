<template>
  <div class="popup">
    <div class="popup__background">
      <div class="popup__content">
        <h2 v-if="status">{{ resolveMessage }}</h2>
        <h2 v-else>{{ rejectMessage }}</h2>
      </div>
      <div class="popup__footer">
        <button class="close_modal" @click="closePopup">OK</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    status: Boolean,
  },
  data: () => ({
    resolveMessage: "Thank you!",
    rejectMessage: "Something went wrong!",
  }),
  methods: {
    closePopup() {
      this.$emit("closePopup");
    },
  },
};
</script>

<style>
.popup {
  top: 0;
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: black;
}
.popup__background {
  background-color: #f0f0f0;
  text-align: center;
  min-width: 40%;
  width: 60%;
  max-height: 250px;
  height: 100%;
  margin: auto;
  margin-top: 5%;
  padding: 5%;
  border-style: groove;
}
.close_modal {
  width: 100px;
  color: white;
  background-color: #6633ff;
  border-radius: 20px;
  margin: 5% 1% 1% 1%;
  padding: 1%;
}

@media only screen and (max-width: 800px) {
  .popup__background {
    height: 20%;
  }
}
</style>