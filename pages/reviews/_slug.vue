<template>
  <article>
    <nuxt-content :document="review" />
  </article>
</template>

<script>
export default {
  // async asyncData ({ $content }) {
  //   const page = await $content('hello').fetch()
  //
  //   return {
  //     page
  //   }
  // }
  async asyncData({ $content, params }) {
    const review = await $content('reviews', params.slug).fetch();

    return { review };
  }
}
</script>

<style lang="scss" scoped>
article {
  display: block;
  margin: 0 auto;
  padding: 50px 30px;
  max-width: 800px;
}

h1 {
  font-size: 28px;
  font-weight: 800;
  margin-bottom: 30px;
}
</style>
