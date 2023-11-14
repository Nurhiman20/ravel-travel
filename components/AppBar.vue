<template>
  <v-app-bar class="px-10" :elevation="1">
    <div>
      <div class="d-flex flex-row align-center logo">
        <img class="logo--image" src="@/assets/images/logo.png" alt="logo">
        <div class="d-flex flex-column ml-3 logo--title">
          <p class="font-weight-black">Ravel</p>
          <p class="mt-n1 text-body-2">Travel Solution by Randy</p>
        </div>
      </div>
    </div>
    <v-spacer />
    <div class="d-flex flex-row">
      <nuxt-link to="/" class="px-4">Home</nuxt-link>
      <nuxt-link to="/test" class="px-4">Tempat Lain</nuxt-link>
      <nuxt-link to="/test2" class="px-4">Testimoni</nuxt-link>
    </div>
    <v-spacer />
    <div class="d-flex flex-row align-center">
      <p class="mr-3">Halo, Reza</p>
      <v-avatar color="blue">
        <span class="text-h6">RP</span>
      </v-avatar>
    </div>
  </v-app-bar>
</template>

<script setup>
</script>

<style lang="scss" scoped>
.logo {
  &--image {
    width: 45px;
    height: 40px;
  }
}

a {
  text-decoration: none;
  color: black;
  font-weight: 600;
  &:hover {
    opacity: 0.8;
  }
}
.router-link-active {
  color: #4BFF72;
}
</style>
