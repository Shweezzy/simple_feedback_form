<template>
  <v-app>
    <FeedbackForm :rating="this.rating">
      <RateUs @asd="cas" />
    </FeedbackForm>
  </v-app>
</template>

<script>
import FeedbackForm from "./components/FeedbackForm";
import RateUs from "./components/RateUs";

export default {
  name: "App",

  components: { FeedbackForm, RateUs },

  data: () => ({
    rating: 2,
  }),
  methods: {
    cas(data) {
      this.rating = data.rating;
    },
  },
};
</script>
