<template>
  <div class="explosion-button">
    <b-button v-show="!explosion" ref="button" class="btn" @click="showExplosion">Click Me</b-button>

    <div class="explosion" v-show="explosion">
      <img src="img/explsion.gif" alt="" >
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      explosion: false,
    }
  },
  methods: {
    showExplosion() {
      this.explosion = true;
      setTimeout(() => {
        this.explosion = false;
      }, 750);
    },
  },
};
</script>

<style lang="scss" scoped>
.explosion-button {
  display: inline-block;
  position: absolute;

}

.btn {
  //background-color: $deep-purple;
}
.explosion {
  position: absolute;
  top: -12px;
  z-index: 1;
}

img {
  width: 90px;
}
</style>
