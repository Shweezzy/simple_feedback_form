<template>
  <div>
    <v-form class="d-flex form" v-model="valid">
      <v-container>
        <h1 id="form__title">FEEDBACK FORM</h1>
        <v-text-field
          v-model="firstName"
          :rules="dataRules"
          label="Name"
          solo
        ></v-text-field>
        <span :messages="['Message']"></span>
        <v-text-field
          v-model="email"
          :rules="emailRules"
          label="Email"
          solo
          required
        ></v-text-field>
        <slot></slot>
        <v-textarea
          v-model="comment"
          :rules="dataRules"
          label="Comment"
          no-resize
          solo
        ></v-textarea>
        <v-btn
          @click="sendData"
          :disabled="!valid"
          class="btn m-auto"
          elevation="2"
          color="#6633FF"
          rounded
          >Send Feedback</v-btn
        >
      </v-container>
    </v-form>

    <!-- Vue Modal -->
    <PopupInfo
      :status="checkStatus"
      v-if="showModal"
      @closePopup="closeResolvePopup"
    />

    <!-- bootstrap -->
    <b-modal v-model="resolveBootstrapModal" ok-only>
      <h2>Thank you!</h2>
    </b-modal>
    <b-modal v-model="rejectBootstrapModal" ok-only>
      <h2>Something went wrong!</h2>
    </b-modal>
  </div>
</template>

<script>
// import axios from "axios";

import PopupInfo from "./popup/PopupInfo.vue";

export default {
  components: {
    PopupInfo,
  },
  props: {
    rating: Number,
  },
  data: () => ({
    checkStatus: false,
    showModal: false,

    rejectBootstrapModal: false,
    resolveBootstrapModal: false,

    valid: false,
    firstName: "",
    comment: "",
    email: "",
    emailRules: [
      (r) => !!r || "E-mail is required",
      (r) =>
        /(^[^0-9]\w+)@(\w+)\.(\w)/g.test(r) ||
        "Please paste correct email address",
    ],
    dataRules: [(r) => !!r || "Data is required"],
  }),
  methods: {
    sendData() {
      // const request = {
      //   name: this.firstName,
      //   email: this.email,
      //   rating: this.rating,
      //   comment: this.comment,
      // };
      // axios
      //   .post("https://it-academy-viseven.herokuapp.com/task6-check", request)
      //   .then((response) => {
      //     console.log("Status:", response.status);
      //     this.showModal = !this.showModal;
      //     if (response.status === 200) {
      //       this.checkStatus = true;
      //     } else {
      //       this.checkStatus = false;
      //     }
      //     console.log(response.data);
      //   })
      //   .catch((error) => {
      //     this.errorMessage = error.message;
      //     console.error("There was an error!", error);
      //   });

      const request = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          name: this.firstName,
          email: this.email,
          rating: this.rating,
          comment: this.comment,
        }),
      };
      fetch("https://it-academy-viseven.herokuapp.com/task6-check", request)
        .then((response) => {
          console.log("Status:", response.status);
          this.showModal = !this.showModal;
          if (response.status === 200) {
            this.checkStatus = true;
          } else {
            this.checkStatus = false;
          }
          // if (response.status == 200) {
          //   this.resolveBootstrapModal = !this.resolveBootstrapModal;
          // } else {
          //   this.rejectBootstrapModal = !this.rejectBootstrapModal;
          // }
          return response.json();
        })
        .then((data) => {
          console.log(data);
        });
    },
    closeResolvePopup() {
      this.showModal = !this.showModal;
    },
  },
};
</script>

<style>
form {
  text-align: center;
  width: 600px;
  margin: auto;
  margin-top: 3%;
  background: #f0f0f0;
  border-style: groove;
}
#form__title {
  margin-top: 2%;
  margin-bottom: 5%;
}
.v-application--is-ltr .v-rating .v-icon {
  font-size: 34px;
}
.v-text-field.v-text-field--solo .v-label {
  color: black;
  resize: none;
}
.v-text-field.v-text-field--enclosed:not(.v-text-field--rounded) {
  width: 80%;
  margin: auto;
}
.v-btn:not(.v-btn--round).v-size--default {
  width: 40%;
  border-radius: 20px;
}
.v-btn span {
  color: white;
  text-transform: capitalize;
}
.modal-content {
  text-align: center;
  background-color: #f0f0f0;
}
#__BVID__24___BV_modal_header_,
#__BVID__24___BV_modal_footer_,
#__BVID__25___BV_modal_header_,
#__BVID__25___BV_modal_footer_ {
  border: none;
  margin: auto;
}
#__BVID__24___BV_modal_content_ {
  background-color: #f0f0f0;
}
#__BVID__24___BV_modal_footer_ .btn-primary,
#__BVID__25___BV_modal_footer_ .btn-primary {
  width: 200px;
  border: none;
  border-radius: 20px;
  background-color: #6633ff;
}
.close {
  display: none;
}
</style>