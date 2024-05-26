<template>
  <div class="page-scroll home">
    <HomeHeader></HomeHeader>
    <HomeTexts></HomeTexts>
  </div>
</template>

<script setup lang="ts">
  import HomeHeader from './part/HomeHeader.vue'
  import HomeTexts from './part/HomeTexts.vue'
</script>

<style lang="scss" scoped>
  .home {
    width: 100%;
    padding: $spacing 0;
  }
</style>
