<template>
  <v-app>
    <FeedbackForm><RateUs /></FeedbackForm>
  </v-app>
</template>

<script>
import FeedbackForm from "./components/FeedbackForm";
import RateUs from "./components/RateUs.vue";

export default {
  name: "App",

  components: { FeedbackForm, RateUs },

  data: () => ({
    //
  }),
};
</script>
