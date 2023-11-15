<template>
  <div>
    <div class="w-100 hero">
      <v-img src="@/assets/images/hero.png" width="100%"></v-img>
      <div class="d-flex flex-column hero__title">
        <h1 class="text-white hero__title--main">Ravel</h1>
        <p class="font-weight-bold text-white hero__title--sub">Travel Solution</p>
      </div>
    </div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
.hero {
  position: relative;
  &__title {
    position: absolute;
    bottom: 19px;
    left: 96px;
    &--main {
      font-size: 40px;
    }
    &--sub {
      font-size: 24px;
    }
  }
}
</style>
