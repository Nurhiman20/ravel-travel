<template>
  <div>
    <section id="hero">
      <div class="w-100 hero">
        <v-img src="@/assets/images/hero.png" width="100%"></v-img>
        <div class="d-flex flex-column hero__title">
          <h1 class="text-white hero__title--main">Ravel</h1>
          <p class="font-weight-bold text-white hero__title--sub">Travel Solution</p>
        </div>
      </div>
    </section>

    <section id="new-tour" data-cy="header-new-tour">
      <v-row no-gutters class="px-12 py-9">
        <v-col cols="12" md="4">
          <v-card class="rounded-xl mb-3" width="100%" height="318px">
            <v-img :src="data.data.image" width="100%" cover></v-img>
          </v-card>
        </v-col>
        <v-col cols="12" md="8">
          <div class="d-flex flex-column px-6">
            <h2>Tujuan <span class="text-secondary">Baru</span>!</h2>
            <p class="font-weight-bold mt-2">{{ data.data.name }}</p>
            <p class="mt-3">{{ data.data.description }}</p>
          </div>
        </v-col>
      </v-row>
    </section>
  </div>
</template>

<script setup>
const token = useCookie("token");

const { data } = await useFetch("https://bio-code.cyclic.app/api/v1/tours/new-tour", {
  headers: {
    authorization: `Bearer ${token.value}`,
  },
});
console.log(data);
</script>

<style lang="scss" scoped>
.hero {
  position: relative;
  &__title {
    position: absolute;
    bottom: 19px;
    left: 48px;
    &--main {
      font-size: 40px;
    }
    &--sub {
      font-size: 24px;
    }
  }
}
</style>
