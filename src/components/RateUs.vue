<template>
  <div class="text-center" @click="numberOfStars">
    <h2>RATE US</h2>
    <v-rating
      v-model="rating"
      color="warning"
      background-color="grey lighten-2"
      hover
    ></v-rating>
    <div>
      <span class="font-weight-bold rating">
        {{ rating }}
      </span>
      <span class="font-weight-bold">of {{ length }}</span>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    rating: 2,
    length: 5,
  }),
  methods: {
    numberOfStars() {
      this.$emit("numberOfStars", {
        rating: this.rating,
      });
    },
  },
};
</script>

<style>
.text-center {
  margin-bottom: 3%;
}
</style>