<template>
  <div>
    <section class="header">
      <b-container fluid="xl">

        <!-- Breadcrumb navigation -->
        <nav aria-label="breadcrumb">
          <ol class="breadcrumb">
            <li v-for="(breadcrumb, index) in breadcrumbs" :key="index" class="breadcrumb-item">
              <b-link :to="breadcrumb.path">{{ breadcrumb.label }}</b-link>
            </li>
          </ol>
        </nav>

        <div class="p-0 bg-transparent">
          <h2>Reviews</h2>
          <p></p>
        </div>

        <div class="search d-flex align-center justify-end">
          <b-input-group class="align-items-center">
            <!-- Prepend button with search icon -->
            <b-input-group-prepend is-text class="p-0">
              <b-button size="sm" variant="outline-secondary">
                <b-icon-search></b-icon-search>
              </b-button>
            </b-input-group-prepend>

            <!-- Search input -->
            <b-form-input
              v-model="search"
              type="search"
              class="h-100"
              hide-details="auto"
              placeholder="Search reviews"
              @click:append="clearSearch"
            />
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
            :style="{ borderColor: selectedCategory !== category ? 'transparent' : '' }"
            class="ml-2 mr-2 mb-2"
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
            <b-jumbotron lead="No posts found, yet." class="text-center">

              <template #header>
                <b-icon-search></b-icon-search>
              </template>
              <p>Sorry, I can't find that right now. <span class="emoji">😬</span></p>

            </b-jumbotron>

          </b-col>
        </b-row>

        <b-row v-if="posts.length" class="post-pagination">
          <b-col class="text-right" cols="12">
            <b-btn size="sm" :disabled="page === 1" @click="fetchPrevious">
              <b-icon-arrow-left />
              Previous
            </b-btn>
            <b-btn size="sm" :disabled="!nextPage" @click="fetchNext">
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
    const posts = fetchedPosts;

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
    breadcrumbs() {
      const breadcrumbs = [
        { label: 'Home', path: '/' }, // Assuming this is your home page path
        { label: 'Reviews', path: '/reviews' }, // Assuming this is the path to your reviews page
        // Add more breadcrumb items dynamically based on selectedCategory and search query
        // { label: this.selectedCategory, path: `/reviews/${this.selectedCategory.toLowerCase()}` },
        // // Add breadcrumb item for search query if present
        // ...(this.search ? [{ label: `Search: ${this.search}`, path: '#' }] : []),
      ];
      return breadcrumbs;
    },
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

.search {
  font-size: 1.2rem;

  .input-group {
    > .form-control {
      padding: 0 1rem;
    }
  }

  .input-group-text {
    padding: 0;
  }

  .btn {
    border: 0;
  }
}
</style>
