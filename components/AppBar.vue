<template>
  <v-app-bar class="px-10" :elevation="1">
    <div>
      <div
        class="d-flex flex-row align-center logo pointer"
        data-cy="h-logo"
        @click="router.push('/')"
      >
        <img class="logo--image" src="@/assets/images/logo.png" alt="logo" />
        <div class="d-flex flex-column ml-3 logo--title">
          <p class="font-weight-black">Ravel</p>
          <p class="mt-n1 text-body-2">Travel Solution by Randy</p>
        </div>
      </div>
    </div>
    <v-spacer />
    <div class="d-flex flex-row">
      <nuxt-link to="/" class="px-4" data-cy="h-nav-home">Home</nuxt-link>
      <nuxt-link to="/other-place" class="px-4" data-cy="h-nav-other-place"
        >Tempat Lain</nuxt-link
      >
      <nuxt-link to="/testimoni" class="px-4" data-cy="h-nav-testimoni"
        >Testimoni</nuxt-link
      >
    </div>
    <v-spacer />
    <v-menu>
      <template v-slot:activator="{ props }">
        <div class="d-flex flex-row align-center pointer" data-cy="h-profile" v-bind="props">
          <p class="mr-3">Halo, {{ user.name }}</p>
          <v-avatar color="blue">
            <span class="text-h6">{{ initialName }}</span>
          </v-avatar>
        </div>
      </template>
      <v-list>
        <v-list-item @click="logout">Logout</v-list-item>
      </v-list>
    </v-menu>
  </v-app-bar>
</template>

<script setup>
const props = defineProps({
  user: {
    type: Object,
    required: true,
  },
});
const emit = defineEmits(["logout"]);

const router = useRouter();

const initialName = computed(() => {
  // Split the input string into an array of words
  const words = props.user.name.split(" ");

  // Get the first character of each word and join them
  const initials = words.map((word) => word[0]).join("");

  return initials;
});

const logout = () => {
  emit("logout");
};
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
  color: #4bff72;
}
</style>
