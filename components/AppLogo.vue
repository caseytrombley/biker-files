<template>
  <div class="app-logo">
    <div class="name">Biker Files</div>

  </div>
</template>

<script>
export default {
  name: 'AppLogo',
  props: {
    height: {
      type: Number,
      default: 60
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
    transition: .3s;
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
