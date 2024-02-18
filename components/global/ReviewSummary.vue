<template>
  <div class="review-summary">
    <h1 class="text-4xl">
      <ContentSlot :use="$slots.title" />
    </h1>
    <ContentSlot :use="$slots.description" />
    <ContentSlot :use="$slots.default" />
<!--    <slot />-->
  </div>
</template>

<script>
export default {
  name: 'ReviewSummary'
}
</script>

<style lang="scss" scoped>
.review-summary {
  color: darkgreen;
}
</style>
