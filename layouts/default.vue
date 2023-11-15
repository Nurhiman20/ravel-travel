<template>
  <div>
    <app-bar :user="user" @logout="logout" />
    <main class="pt-16">
      <slot />
    </main>
  </div>
</template>

<script setup>
const user = ref();

const token = useCookie('token');
const router = useRouter();
if (!token.value) {
  router.push('/login')
}

const userId = useCookie('userId');
const { data: userData } = await useFetch('https://bio-code.cyclic.app/api/v1/users', {
  headers: {
    authorization: `Bearer ${token.value}`
  }
});

userData.value.data.forEach(element => {
  if (element.userId == userId.value) {
    user.value = element;
  }
});

const logout = () => {
  token.value = '';
  router.push('/login');
}
</script>
