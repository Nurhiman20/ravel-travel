<template>
  <v-row no-gutters>
    <v-col cols="12" md="6">
      <v-img src="@/assets/images/login-image.png" cover :max-height="'100vh'"></v-img>
    </v-col>
    <v-col cols="12" md="6">
      <v-card class="ma-9 pa-6 d-flex flex-column rounded-xl">
        <div class="d-flex flex-row align-center mx-auto">
          <img class="logo" src="@/assets/images/logo.png" alt="" />
          <div class="d-flex flex-column ml-1">
            <p class="text-h2 font-weight-bold">Ravel</p>
            <p class="text-caption">Travel Solution by Randy</p>
          </div>
        </div>
        <div class="d-flex flex-column mt-6">
          <h2>Masuk</h2>

          <v-form v-model="form" @submit.prevent="onSubmit">
            <div class="text-subtitle-1 text-medium-emphasis mt-3">User ID</div>
            <v-text-field
              v-model="userId"
              density="compact"
              variant="outlined"
              data-cy="input-userId"
              :rules="[required]"
              @input="formatUserId"
            ></v-text-field>

            <div class="text-subtitle-1 text-medium-emphasis mt-1">Password</div>
            <v-text-field
              v-model="password"
              density="compact"
              variant="outlined"
              type="password"
              data-cy="input-password"
              :rules="[required]"
            ></v-text-field>

            <v-checkbox v-model="rememberMe" label="Ingat saya" data-cy="input-remember_me"></v-checkbox>

            <v-btn type="submit" block color="primary" size="large" data-cy="btn-login" :loading="loading">
              Log In
            </v-btn>
          </v-form>

          <p class="mx-auto font-weight-medium mt-3">atau</p>

          <p class="mx-auto font-weight-medium mt-3">
            Belum punya akun?
            <span
              class="text-secondary pointer"
              data-cy="btn-register"
              @click="router.push('/register')"
              >Daftar</span
            >
          </p>
        </div>
      </v-card>
    </v-col>
  </v-row>

  <v-snackbar v-model="showSnackbar" :timeout="3000" :color="isSuccess ? 'secondary' : 'error'" elevation="24">
    {{ message }}
  </v-snackbar>
</template>

<script setup>
definePageMeta({
  layout: "guest",
});
const router = useRouter();

const form = ref(false);
const required = (v) => {
  return !!v || "Wajib diisi!";
};
const password = ref("");
const rememberMe = ref(false);
const userId = ref("");
const formatUserId = () => {
  // Remove spaces and replace with dots
  userId.value = userId.value.replace(/\s+/g, ".");

  // Allow only alphanumeric and dot
  userId.value = userId.value.replace(/[^a-zA-Z0-9.]/g, "");

  // Ensure dots are not added consecutively
  userId.value = userId.value.replace(/\.+/g, ".");
};

const loading = ref(false);
const showSnackbar = ref(false);
const message = ref("");
const isSuccess = ref(false);
const onSubmit = async () => {
  if (!form.value) return;
  loading.value = true;
  const { data, status } = await useFetch(
    "https://bio-code.cyclic.app/api/v1/auam/login",
    {
      method: "post",
      body: {
        userId: userId.value,
        password: password.value,
      },
    }
  );
  
  if (status.value == 'error') {
    message.value = "Id & Password Salah";
    isSuccess.value = false;
    showSnackbar.value = true;
  } else {
    message.value = `Selamat Datang, ${data.value.data.name}`;
    isSuccess.value = true;
    showSnackbar.value = true;
    setTimeout(() => {
      router.push("/");
    }, 3000);
  }
  loading.value = false;
};
</script>

<style lang="scss" scoped>
.logo {
  width: 132px;
  height: 98px;
  object-fit: contain;
}

.pointer {
  &:hover {
    opacity: 0.8;
    cursor: pointer;
  }
}
</style>
