<template>
  <b-container style="max-width: 1000px" fluid>
    <section class="my-3 pt-5">
      <b-btn @click="to()">Go Back</b-btn>
    </section>
    <section class="post-content mt-5">
      <div class="summary">
        <b-row>
          <b-col>
            <h2 class="text-h2 mb-10">{{ post.title }}</h2>
          </b-col>
          <b-col>
            <ul>
              <li v-if="post.motor">{{ post.motor }}</li>
              <li v-if="post.wattage">{{ post.wattage }}W</li>
              <li v-if="post.battery">{{ post.battery }}Wh battery</li>
              <li v-if="post.range">{{ post.range }} mile range</li>
            </ul>


          </b-col>
        </b-row>
      </div>

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
  name: 'ReviewPage',
  layout: 'DefaultLayout',
  async asyncData({ $content, error, params }) {
    try {
      const posts = await $content('reviews').sortBy('createdAt', 'desc').fetch();
      const currentIndex = posts.findIndex(p => p.slug === params.slug);

      if (currentIndex === -1) {
        error({
          statusCode: 404,
          message: 'Post not found.',
        });
        return;
      }

      const post = posts[currentIndex];
      const prev = currentIndex === 0 ? null : posts[currentIndex - 1];
      const next = currentIndex === posts.length - 1 ? null : posts[currentIndex + 1];

      return {
        post,
        prev,
        next,
      };
    } catch (err) {
      console.error('Error fetching posts:', err);
      error({
        statusCode: 500,
        message: 'Internal Server Error',
      });
    }
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
  methods: {
    to() {
      this.$router.push('/reviews')
    },
  },
}
</script>


<style></style>
