<template>
  <div class="app-logo">
    <img
      :src="require(`~/assets/img/logo-bikefiles.svg`)"
      alt="Bike Files"
      :style="{height: getHeight}"
    >
  </div>
</template>

<script>
export default {
  name: 'AppLogo',
  props: {
    height: {
      type: Number,
      default: 50
    }
  },
  computed: {
    getHeight() {
      return `${this.height}px`
    }
  }
}
</script>

<style lang="scss" scoped>
.app-logo {

  .name {
    font-size: 2rem;
    font-weight: 700;
    color: white !important;

  }

  svg {
    transition: all .3s;
    width: auto;
    //height: 60px;
    margin: 0;
    padding: 0;

    @media (max-width: 767px) {
      height: 50px;
    }
  }
}
</style>
