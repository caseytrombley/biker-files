<template>
  <div>
    <section class="header">
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
        <b-row class="justify-content-center mt-5 mb-4">
          <!-- Category buttons -->
          <b-button
            v-for="category in categories"
            :key="category"
            :variant="selectedCategory === category ? 'outline-primary' : 'outline-secondary'"
            class="ml-3"
            style="width: 200px"
            pill
            @click="selectedCategory = category; fetchPosts()"
          >
            {{ category }}
          </b-button>
        </b-row>
        <b-row>
          <b-col v-for="post in filteredPosts" :key="post.slug" cols="12" md="4">
            <BaseCard
              :title="post.title"
              :description="post.description"
              :img="post.img"
              :path="post.path"
            >
              <div class="post-highlights">
                <b-row>
                  <b-col>
                    {{ post.motor }}
                  </b-col>
                  <b-col>
                    {{ post.range }}
                  </b-col>
                  <b-col>
                    {{ post.price }}
                  </b-col>
                </b-row>
              </div>
            </BaseCard>

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
import BaseCard from "~/components/base/BaseCard.vue";

export default {
  name: 'ReviewsHome',
  components: {BaseCard},
  async asyncData({ $content }) {
    const limit = 6;
    const page = 1;

    const fetchedPosts = await $content('reviews')
      .limit(limit)
      .sortBy('createdAt', 'desc')
      .fetch();

    const nextPage = fetchedPosts.length === limit;
    const posts = nextPage ? fetchedPosts.slice(0, -1) : fetchedPosts;

    return {
      page,
      limit,
      posts,
      nextPage,
      categories: ['All Reviews', 'Hub Drive', 'Mid-drive', 'Step-thru', 'Full Suspension'],
    };
  },

  data() {
    return {
      selectedCategory: 'All Reviews',
      search: '',
    };
  },

  computed: {
    filteredPosts() {
      let filtered = this.posts;

      if (this.selectedCategory !== 'All Reviews') {
        filtered = filtered.filter(post => post.categories.includes(this.selectedCategory));
      }

      const searchQuery = this.search.trim().toLowerCase();
      if (searchQuery) {
        filtered = filtered.filter(post => {
          const isInTitle = post.title.toLowerCase().includes(searchQuery);
          const isInDescription = post.description.toLowerCase().includes(searchQuery);
          const isInTags = post.tags.some(tag => tag.toLowerCase().includes(searchQuery));
          return isInTitle || isInDescription || isInTags;
        });
      }

      return filtered;
    },
  },

  watch: {
    selectedCategory() {
      this.page = 1; // Reset page to 1 when category changes
      this.fetchPosts();
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

      if (this.selectedCategory !== 'All Reviews') {
        baseFetch = baseFetch.where({ categories: { $contains: this.selectedCategory } });
      }

      const fetchedPosts = await baseFetch
        .sortBy('createdAt', 'desc')
        .skip(this.limit * (this.page - 1)) // Adjusted skip calculation
        .fetch();

      this.nextPage = fetchedPosts.length === this.limit;
      this.posts = fetchedPosts; // No need to slice here
    },
    clearSearch() {
      this.search = '';
    },
  },
};
</script>

<style lang="scss" scoped>
.header {
  padding: 2rem 0;
}
[class^="col-"] {
  display: flex;
  flex-direction: column;
}
</style>
