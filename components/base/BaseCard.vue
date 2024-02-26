<template>
  <router-link :to="path" class="base-card-link">
    <b-card elevation="0" class="base-card">
      <b-card-title>{{ title }}</b-card-title>
      <div>{{ description }}</div>
      <b-card-img
        :src="require(`~/assets/img/reviews/${img}`)"
        :alt="title" width="100%"
      />
      <b-card-text>
        <slot />
      </b-card-text>
      <div>
        <b-btn text :to="path">Read More</b-btn>
      </div>
    </b-card>
  </router-link>

</template>

<script>
export default {
  name: 'BaseCard',
  props: {
    title: {
      type: String,
      default: ''
    },
    img: {
      type: String,
      default: ''
    },
    description: {
      type: String,
      default: ''
    },
    path: {
      type: String,
      default: ''
    },
  }
}
</script>

<style lang="scss" scoped>
.base-card-link {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  text-decoration: none;
  color: inherit;
}
.base-card {
  position: relative;
  display: flex;
  flex-direction: column;
  flex-grow: 1; // Allow cards to grow to fill container height
  min-width: 0;
  margin-bottom: 1.5rem;
  word-wrap: break-word;
  background-color: #fff;
  background-clip: border-box;
  border-radius: 1.25rem;
  border: 1px solid #d5d8dc;
  transition: all .3s;

  &:hover {
    box-shadow: 0 0 0 8px rgba(108, 117, 125, 0.07);
    border: 1px solid #d0d2d3;
  }

  ::v-deep {
    .card-body {
      display: flex;
      flex-direction: column;
      flex-grow: 1;
    }
  }

  img {
    margin-top: auto;
  }
}
</style>
