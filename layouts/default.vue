<template>
  <div>
    <app-bar v-if="user" :user="user" @logout="logout" />
    <main class="pt-16">
      <slot />
    </main>
  </div>
</template>

<script setup>
const user = ref();

const router = useRouter();
const token = useCookie('token');
if (!token.value) {
  router.push('/login')
}

const userId = useCookie('userId');
const { data: userData } = await useFetch('https://bio-code.cyclic.app/api/v1/users', {
  headers: {
    authorization: `Bearer ${token.value}`
  }
});

if (userData.value) {
  userData.value.data.forEach(element => {
    if (element.userId == userId.value) {
      user.value = element;
    }
  });
}

const logout = () => {
  token.value = '';
  router.push('/login');
}
</script>
