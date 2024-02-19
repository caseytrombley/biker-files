<template>
  <div>
    <section>
      <b-container fluid="xl">
        <h1>Reviews home</h1>

        <div class="search d-flex align-center justify-end">
          <b-input-group size="sm" class="align-items-center">
            <b-form-input v-model="search" type="search" hide-details="auto" placeholder="Search for a post" @click:append="clearSearch" />
          </b-input-group>
        </div>
      </b-container>
    </section>
    <section>
      <b-container fluid="xl">
        <b-row>
          <b-form-select
            v-model="selectedCategory"
            :options="categories"
            hide-details="auto"
            class="ml-3"
            style="width: 200px"
          />
        </b-row>
        <b-row>
          <b-col v-for="post in filteredPosts" :key="post.slug" cols="12" md="6">
            <b-card elevation="0">
              <b-card-title>{{ post.title }}</b-card-title>
              <b-card-subtitle>{{ post.description }}</b-card-subtitle>
              <b-card-text>
<!--                {{-->
<!--                  new Intl.DateTimeFormat('en-US', {-->
<!--                    year: 'numeric',-->
<!--                    month: 'numeric',-->
<!--                    day: 'numeric',-->
<!--                    hour: 'numeric',-->
<!--                    minute: 'numeric',-->
<!--                    second: 'numeric',-->
<!--                  }).format(new Date(post.createdAt))-->
<!--                }}-->
<!--                <ul>-->
<!--                  <li v-for="(value, key) in post" :key="key">-->
<!--                    <strong>{{ key }}:</strong> {{ value }}-->
<!--                  </li>-->
<!--                </ul>-->
              </b-card-text>
              <b-card-img :src="require(`~/assets/img/reviews/${post.img}`)" :alt="post.title" width="100%" />
              <b-card-actions>
                <b-btn text :to="post.path">Read More</b-btn>
              </b-card-actions>
            </b-card>
          </b-col>
        </b-row>
        <b-row v-if="filteredPosts.length === 0">
          <b-col cols="12">
            <p>No posts found, yet. <span class="emoji">😁</span></p>
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
    const limit = 5;
    const page = 1;

    const fetchedPosts = await $content('reviews')
      .limit(limit)
      .sortBy('createdAt', 'desc')
      .skip((limit - 1) * (page - 1))
      .fetch();

    const nextPage = fetchedPosts.length === limit;
    const posts = nextPage ? fetchedPosts.slice(0, -1) : fetchedPosts;

    // Extract unique categories from all posts
    const allCategories = posts.reduce((categories, post) => {
      categories.push(...post.categories);
      return categories;
    }, []);

    const uniqueCategories = [...new Set(allCategories)];

    return {
      page,
      limit,
      posts,
      nextPage,
      categories: ['all', ...uniqueCategories], // Include 'all' option
    };
  },

  data() {
    return {
      selectedCategory: 'all',
      search: '',
    };
  },

  computed: {
    filteredPosts() {
      let filtered = this.posts;

      if (this.selectedCategory !== 'all') {
        filtered = filtered.filter(post => post.categories.includes(this.selectedCategory));
      }

      if (this.search.trim() !== '') {
        filtered = filtered.filter(post =>
          post.title.toLowerCase().includes(this.search.toLowerCase())
        );
      }

      return filtered;
    },
  },

  methods: {
    async fetchNext() {
      this.page += 1;
      await this.fetchPosts();
    },
    async fetchPrevious() {
      this.page -= 1;
      await this.fetchPosts();
    },
    async fetchPosts() {
      let baseFetch = this.$content('reviews').limit(this.limit);

      if (this.selectedCategory !== 'all') {
        baseFetch = baseFetch.where({ categories: { $contains: this.selectedCategory } });
      }

      const fetchedPosts = await baseFetch
        .sortBy('createdAt', 'desc')
        .skip((this.limit - 1) * (this.page - 1))
        .fetch();

      this.nextPage = fetchedPosts.length === this.limit;
      this.posts = this.nextPage ? fetchedPosts.slice(0, -1) : fetchedPosts;
    },
    clearSearch() {
      this.search = '';
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
