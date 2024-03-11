<template>
  <router-link :to="path" class="base-card-link">
    <b-card elevation="0" class="base-card">


      <b-card-img
        :src="require(`~/assets/img/reviews/${img}`)"
        :alt="title" width="100%"
      />

      <b-card-title>
        <div class="title">{{ title }}</div>
        <div class="sub text-muted">{{ description }}</div>

      </b-card-title>
<!--      <b-card-text>-->
<!--        <slot />-->
<!--      </b-card-text>-->
      <div v-if="highlights" class="post-highlights align-height">
        <div class="wrapper">
          <b-row>
            <b-col>
              <b-form-rating
                v-if="highlights.rating"
                v-model="rating"
                precision="2"
                readonly
                size="md"
                class="rating"
                variant="warning"
              />
              <div v-else class="text-muted">Unrated</div>
              <div class="label">Rating</div>

            </b-col>
            <b-col>
              <div class="val">{{ highlights.motor }}</div>
              <div class="label">Motor</div>
            </b-col>
            <b-col>
              <div class="val">{{ highlights.range }} mi</div>
              <div class="label">Range</div>
            </b-col>

          </b-row>
        </div>
      </div>
<!--      <div>-->
<!--        <b-btn size="sm" text :to="path">Read More</b-btn>-->
<!--      </div>-->
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
    highlights: {
      type: Object,
      default() {
        return {}
      }
    },
  },
  data() {
    return {
      rating: this.highlights.rating
    }
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

  .align-height {
    margin-top: auto;
  }

  .sub {
    font-size: .685em;
    margin-top: .5rem;
  }

  ::v-deep {
    .card-title, .card-text, .card-img {
      padding: 1.25rem;
    }
    .card-body {
      display: flex;
      flex-direction: column;
      flex-grow: 1;
      padding: 0;
    }
  }

}

.post-highlights {

  .wrapper {
    padding: 1.25rem;
    border-top: .5px solid #d5d8dc;
  }

  .val {
    height: 1.5rem;
  }
  .label {
    font-size: .75rem;
    color: #6c757d;
  }
}

.rating {
  padding: 0;
  border: 0;
  width: 0;
  height: 1.5rem !important;
}

::v-deep {
  .b-rating .b-rating-star,
  .b-rating .b-rating-value {
    padding: 0 0.0125em;
  }
}
</style>
