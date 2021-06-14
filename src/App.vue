<template>
  <v-app>
    <FeedbackForm :rating="this.rating">
      <!-- <RateUs @numberOfStars="updateRating" /> -->
      <RateUs2 @numberOfStars="updateRating" :grade="2" />
    </FeedbackForm>
  </v-app>
</template>

<script>
import FeedbackForm from "./components/FeedbackForm";
// import RateUs from "./components/RateUs";
import RateUs2 from "./components/RateUs2.vue";
export default {
  name: "App",

  components: { FeedbackForm, RateUs2 },

  data: () => ({
    rating: 7,
  }),
  methods: {
    updateRating(data) {
      this.rating = data.rating;
    },
  },
};
</script>
