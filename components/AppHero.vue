<template>
  <div class="hero-section" :class="getCss">
<!--    <video v-if="showVideo" class="hero-video" autoplay muted loop>-->
<!--      <source :src="videoSource" type="video/mp4">-->
<!--    </video>-->
    <div class="content">
      <h1>It's a wild ride</h1>
      <p>
        Navigate adrenaline-fueled tales, explore gear essentials, and delve into the raw, unfiltered world of two-wheeled exploration.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppHero',
  data() {
    return {
      showVideo: false,
      // videoSource: '/video/mtb-web.mp4',
    };
  },
  computed: {
    getCss() {
      return !this.showVideo ? 'colorBg' : null
    }
  },
  methods: {
    toggleBg() {
      this.showVideo = !this.showVideo;
    }
  }
};
</script>

<style lang="scss" scoped>
.hero-section {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;

  &.colorBg {
    background-color: #212529;
  }

  &:before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(138, 3, 156, 0.7);
    mix-blend-mode: color-burn;
  }

  .content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    color: #fff;
  }

  h1 {
    font-size: 48px;
    font-weight: bold;
    margin-bottom: 20px;
  }

  p {
    font-size: 24px;
  }
}

.hero-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
  mix-blend-mode: luminosity;
}
</style>
