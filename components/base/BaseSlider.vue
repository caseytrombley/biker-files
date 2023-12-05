<template>
  <b-carousel
      id="carousel-fade"
      class="slider"
      style="text-shadow: 0px 0px 2px #000"
      fade
      img-width="1024"
      img-height="480"
      interval="3000"
  >
    <b-carousel-slide
        v-for="slide in slides"
        :key="slide.title"
        :caption="slide.title"
        :img-src="slide.image"
    ></b-carousel-slide>

  </b-carousel>
</template>

<script>
export default {
  props: {
    carouselId: {
      type: String,
    },
    slides: {
      type: Array,
      default: () => [
        {
          image: '',
          alt: '',
          title: '',
          description: '',
        }
      ]
    },
  },
};
</script>

<style lang="scss">

.carousel-indicators {
  list-style: none;

  li {
    box-sizing: content-box;
    -ms-flex: 0 1 auto;
    flex: 0 1 auto;
    width: 30px;
    height: 3px;
    margin-right: 3px;
    margin-left: 3px;
    text-indent: -999px;
    cursor: pointer;
    background-color: #fff;
    background-clip: padding-box;
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
    opacity: .5;
    transition: opacity .6s ease;

    &::marker {
      display: none;
    }
  }
}

</style>
