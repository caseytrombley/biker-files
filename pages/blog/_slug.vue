<template>
  <b-container style="max-width: 1000px" fluid>
    <section class="my-3 pt-5">
      <b-btn @click="to()">Go Back</b-btn>
    </section>
    <section class="post-content mt-5">
      <h2 class="text-h2 mb-10">{{ post.title }}</h2>
      <nuxt-content :document="post" />
    </section>
    <b-row>
      <b-col class="d-flex justify-space-between align-center mt-5" cols="12">
        <b-btn :disabled="!prev" :to="prev && prev.path">Previous Post</b-btn>
        <b-btn :disabled="!next" :to="next && next.path">Next Post</b-btn>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: 'BlogPostPage',
  layout: 'DefaultLayout',
  async asyncData({ $content, error, params }) {
    const post = await $content('blog', params.slug)
      .fetch()
      .catch(() => {
        error({
          statusCode: 404,
          message: 'Oops, looks like that does not exist...',
        });
      });

    // Fetch previous and next posts based on current post's slug
    const [prev, next] = await $content('blog')
      .only(['path'])
      .sortBy('createdAt', 'desc')
      .surround(params.slug)
      .fetch();

    return {
      post,
      prev,
      next,
    };
  },
  methods: {
    to() {
      window.history.length > 1 ? this.$router.go(-1) : this.$router.push('/')
    },
  },
  head() {
    return {
      title: this.post.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.post.description,
        },
        // Open Graph
        { hid: 'og:title', property: 'og:title', content: this.post.title },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.post.description,
        },
        // Twitter Card
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: this.post.title,
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: this.post.description,
        },
      ],
    }
  },
}
</script>

<style></style>
