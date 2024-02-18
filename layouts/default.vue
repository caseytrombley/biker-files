<template>
  <div class="default">
    <AppHeader />
    <div class="main">
      <Nuxt />
    </div>


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

}
.main {
  padding-top: 70px;
}
</style>
