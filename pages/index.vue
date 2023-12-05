<template>
  <div>
    <AppHero />

    <div class="container-inside">
      <b-container>
        <h2>Latest Posts</h2>

        <div class="articles">
          <div
            class="article"
            v-for="article of articles"
            :key="article"
          >

            <nuxt-link :to="{ name: 'blog-slug', params: { slug: article.slug }}">
              <div class="article-preview">
                <img :src="require(`~/assets/img/blog/${article.img}`)" alt="Blog image">
                <h4>{{ article.title }}</h4>
                <p>{{ article.description }}</p>
              </div>

            </nuxt-link>
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

    return {
      articles
    }
  }
}
</script>

<style lang="scss" scoped>
.article-preview {
  img {
    width: 200px;
  }
}
</style>
