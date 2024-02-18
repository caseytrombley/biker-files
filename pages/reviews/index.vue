<template>
  <div>
    <section>
      <b-container fluid="xl">
        <h1>Reviews home</h1>

        <div
          class="search d-flex align-center justify-end ml-3"
        >
          <b-input-group size="sm" class="align-items-center">
            <!--                <template #prepend>-->
            <!--                  <b-input-group-text><b-icon icon="search"></b-icon></b-input-group-text>-->
            <!--                </template>-->
            <b-form-input
              v-model="search"
              type="search"
              hide-details="auto"
              placeholder="Search for a post"
              @click:append="clearSearch"
            />
          </b-input-group>


        </div>
      </b-container>
    </section>
    <section>
      <b-container fluid="xl">
        <b-row v-if="!posts.length">
          <b-col cols="12">
            <p>No posts found, yet. <span class="emoji">😁</span></p>
          </b-col>
        </b-row>
        <b-row v-else class="posts-container mt-5">
          <b-col cols="12">
            <div class="filter">
              <b-form-select
                v-if="categories.length"
                v-model="category"
                style="width: 100px"
                hide-details="auto"
                :options="categories"
              />
            </div>
          </b-col>

          <b-col v-for="post in posts" :key="post.slug" cols="12" md="6">
            <b-card elevation="0">
              <b-card-title> {{ post.title }} </b-card-title>
              <b-card-subtitle>
                {{
                  new Intl.DateTimeFormat('en-US', {
                    year: 'numeric',
                    month: 'numeric',
                    day: 'numeric',
                    hour: 'numeric',
                    minute: 'numeric',
                    second: 'numeric',
                  }).format(new Date(post.createdAt))
                }}
              </b-card-subtitle>
              <b-card-text>
                <nuxt-content :document="{ body: post.excerpt }" />
              </b-card-text>
              <b-card-actions>
                <b-btn text :to="post.path">Read More</b-btn>
              </b-card-actions>
            </b-card>
          </b-col>
        </b-row>
        <b-row v-if="posts.length" class="post-pagination">
          <b-col class="text-right" cols="12">
            <b-btn :disabled="page === 1" @click="fetchPrevious">
              <b-icon-arrow-left />
              Previous
            </b-btn>
            <b-btn :disabled="!nextPage" @click="fetchNext">
              Next
              <b-icon-arrow-right />
            </b-btn>
          </b-col>
        </b-row>
      </b-container>

    </section>
  </div>
</template>

<script>
export default {
  name: 'ReviewsHome',
  async asyncData({ $content }) {
    const limit = 5
    const page = 1

    const fetchedPosts = await $content('reviews')
      .limit(limit)
      .sortBy('createdAt', 'desc')
      .skip((limit - 1) * (page - 1))
      .fetch()

    const nextPage = fetchedPosts.length === limit
    const posts = nextPage ? fetchedPosts.slice(0, -1) : fetchedPosts

    return {
      page,
      limit,
      posts,
      nextPage,
    }
  },

  data: () => ({
    category: 'all',
    categories: [],
  }),

  fetch() {
    this.$content('reviews')
      .only(['category'])
      .fetch()
      .then((categories) => {
        const payload = Array.from(new Set(categories.map((c) => c.category)))
        this.categories = ['all', ...payload]
      })
  },

  computed: {
    search: {
      get() {
        return this.$store.state.query;
      },
      set(value) {
        // Update Vuex store and trigger post fetching
        this.$store.commit('SET_QUERY', value);
        this.$router.push({ query: { q: value } });
      },
    },
    searchQuery() {
      return this.$store.state.query
    },
  },

  watch: {
    async searchQuery(newValue) {
      this.page = 1
      await this.fetchPosts(newValue)
    },
    async category() {
      this.page = 1
      await this.fetchPosts(this.searchQuery)
    },
  },

  methods: {
    clearSearch() {
      this.$store.commit('SET_QUERY', '')
    },
    async fetchNext() {
      this.page += 1
      await this.fetchPosts()
    },
    async fetchPrevious() {
      this.page -= 1
      await this.fetchPosts()
    },
    async fetchPosts(query = '') {
      let baseFetch = this.$content('reviews').limit(this.limit)

      if (this.category !== 'all') {
        baseFetch = baseFetch.where({ category: this.category })
      }

      const fetchedPosts = await baseFetch
        .search(query)
        .sortBy('createdAt', 'desc')
        .skip((this.limit - 1) * (this.page - 1))
        .fetch()

      this.nextPage = fetchedPosts.length === this.limit
      const posts = this.nextPage ? fetchedPosts.slice(0, -1) : fetchedPosts
      this.posts = posts
    },
  },
}
</script>

<style lang="scss" scoped>

</style>
