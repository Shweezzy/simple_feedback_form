<template>
  <div class="container">
    <h2 class="container__title">RATE US</h2>
    <div class="rating">
      <ul class="list" @click="numberOfStars">
        <li
          :key="star"
          v-for="star in allStars"
          :class="{ active: star <= stars }"
          @click="rate(star)"
          class="star"
        >
          <icon scale="2" :name="star <= stars ? 'star' : 'regular/star'" />
        </li>
      </ul>
      <span v-if="starsCounter">{{ stars }} of {{ allStars }}</span>
    </div>
  </div>
</template>

<script>
import "vue-awesome/icons/star";
import "vue-awesome/icons/regular/star";

import Icon from "vue-awesome/components/Icon";

export default {
  components: { Icon },
  props: {
    grade: {
      type: Number,
      required: true,
    },
    allStars: {
      type: Number,
      default: 5,
    },
    starsCounter: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      stars: this.grade,
    };
  },
  methods: {
    rate(star) {
      this.stars = this.stars === star ? star - 1 : star;
    },
    numberOfStars() {
      this.$emit("numberOfStars", {
        rating: this.stars,
      });
    },
  },
};
</script>
<style scoped lang="scss">
.rating {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 22px;
  color: #a7a8a8;
  text-align: center;
  margin: auto;
}
.rating span {
  color: black;
  font-weight: bolder;
}
.container__title {
  text-align: center;
}
.list {
  margin: 0 0 5px 0;
  padding: 0;
  list-style-type: none;
  &:hover {
    .star {
      color: #f3d23e;
    }
  }
}
.star {
  display: inline-block;
  cursor: pointer;
}
.star:hover {
  & ~ .star {
    &:not(.active) {
      color: inherit;
    }
  }
}
.active {
  color: #f3d23e;
}
.fa-icon {
  width: 50px;
}
</style>
