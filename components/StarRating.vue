<template>
  <div :style="{ fontSize: starSize, fontFamily: starFontFamily }" class="Stars" :aria-label="'Rating of this product is ' + rating + ' out of 5.'">
    <span :style="{ background: starBackground }" class="filledStars"></span>
    <span class="emptyStars"></span>
  </div>
</template>

<script>
export default {
  props: {
    rating: {
      type: String,
      required: true
    },
    starSize: {
      type: String,
      default: '60px'
    },
    starColor: {
      type: String,
      default: '#fff'
    },
    starBackground: {
      type: String,
      default: '#fc0'
    },
    starFontFamily: {
      type: String,
      default: 'Times'
    }
  },
  computed: {
    filledStarsStyle() {
      const percent = parseFloat(this.rating) / 5 * 100 + '%';
      return {
        background: `linear-gradient(90deg, ${this.starBackground} ${percent}, ${this.starColor} ${percent})`,
        WebkitBackgroundClip: 'text',
        WebkitTextFillColor: 'transparent',
        letterSpacing: '3px'
      };
    }
  }
};
</script>

<style scoped>
.Stars {
  display: inline-block;
  line-height: 1;
}

.filledStars {
  display: inline-block;
}

.emptyStars {
  display: inline-block;
  content: '★★★★★';
}
</style>
