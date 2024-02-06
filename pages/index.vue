<template>
  <div>
    <AppHero />

    <div class="container-inside">
      <b-container>
        <div>
          <h2>Latest Reviews</h2>

          <div class="reviews items">
            <div
              v-for="(review, i) of reviews"
              :key="i"
              class="review item"
            >

              <nuxt-link :to="{ name: 'reviews-slug', params: { slug: review.slug }}">
                <div class="item-preview">
                  <img :src="require(`~/assets/img/reviews/${review.img}`)" alt="Review image">
                  <h4>{{ review.title }}</h4>
                  <p>{{ review.description }}</p>
                </div>

              </nuxt-link>
            </div>
          </div>
        </div>
        <div>
          <h2>Latest Posts</h2>

          <div class="articles items">
            <div
              v-for="(article, i) of articles"
              :key="i"
              class="article item"
            >

              <nuxt-link :to="{ name: 'blog-slug', params: { slug: article.slug }}">
                <div class="item-preview">
                  <img :src="require(`~/assets/img/blog/${article.img}`)" alt="Blog image">
                  <h4>{{ article.title }}</h4>
                  <p>{{ article.description }}</p>
                </div>

              </nuxt-link>
            </div>
          </div>
        </div>
      </b-container>

    </div>

  </div>
</template>

<script>

export default {
  name: 'IndexPage',
  async asyncData ({ $content, params }) {
    const articles = await $content('blog', params.slug)
      .only(['title', 'description', 'slug', 'img'])
      .sortBy('createdAt', 'asc')
      .fetch();

    const reviews = await $content('reviews', params.slug)
      .only(['title', 'description', 'slug', 'img'])
      .sortBy('createdAt', 'asc')
      .fetch();

    return {
      articles,
      reviews
    }
  }
}
</script>

<style lang="scss" scoped>
.item-preview {
  img {
    width: 200px;
  }
}
</style>
