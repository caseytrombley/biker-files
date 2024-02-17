<template>
  <div class="default">
    <AppHeader />

    <Nuxt />

    <AppFooter />
  </div>
</template>

<script>
import AppHeader from "~/components/AppHeader";
import AppFooter from "~/components/AppFooter";
export default {
  name: 'DefaultLayout',
  components: {AppFooter, AppHeader},
}
</script>

<style lang="scss" scoped>
::v-deep {
  .container-inside {
    margin: 2rem 0;
  }
}
</style>
