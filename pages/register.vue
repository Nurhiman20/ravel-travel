<template>
  <img class="logo-bg" src="@/assets/images/large-logo.png" alt="logo" />
  <v-card class="ma-auto pa-6 rounded-xl" width="531">
    <h2>Daftar</h2>

    <v-form v-model="form" @submit.prevent="onSubmit">
      <div class="text-subtitle-1 text-medium-emphasis mt-3">User ID</div>
      <v-text-field
        v-model="userId"
        density="compact"
        variant="outlined"
        placeholder="Masukkan User ID"
        data-cy="input-userId"
        :rules="[required]"
        @input="formatUserId"
      ></v-text-field>

      <div class="text-subtitle-1 text-medium-emphasis mt-1">Nama</div>
      <v-text-field
        v-model="userName"
        density="compact"
        variant="outlined"
        placeholder="Masukkan Nama"
        data-cy="input-name"
        :rules="[required]"
      ></v-text-field>

      <div class="text-subtitle-1 text-medium-emphasis mt-1">Password</div>
      <v-text-field
        v-model="password"
        density="compact"
        placeholder="Masukkan password"
        variant="outlined"
        data-cy="input-password"
        :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
        :type="visible ? 'text' : 'password'"
        :rules="[required, matchConfirmation]"
        @click:append-inner="visible = !visible"
      ></v-text-field>

      <div class="text-subtitle-1 text-medium-emphasis mt-1">Konfirmasi Password</div>
      <v-text-field
        v-model="passwordConfirmation"
        density="compact"
        placeholder="Masukkan konfirmasi password"
        variant="outlined"
        data-cy="input-confirmation_password"
        :append-inner-icon="visibleConfirmation ? 'mdi-eye-off' : 'mdi-eye'"
        :type="visibleConfirmation ? 'text' : 'password'"
        :rules="[required, matchConfirmation]"
        @click:append-inner="visibleConfirmation = !visibleConfirmation"
      ></v-text-field>

      <v-btn
        class="mt-3"
        type="submit"
        block
        color="primary"
        size="large"
        data-cy="btn-register"
        :loading="loading"
        >Daftar</v-btn
      >
    </v-form>
  </v-card>
  <v-snackbar v-model="showSnackbar" :timeout="3000" :color="isSuccess ? 'secondary' : 'error'" elevation="24">
    {{ message }}
  </v-snackbar>
</template>

<script setup>
definePageMeta({
  layout: "guest",
});

const visible = ref(false);
const visibleConfirmation = ref(false);

const required = (v) => {
  return !!v || "Wajib diisi!";
};
const matchConfirmation = (v) => {
  if (password.value != passwordConfirmation.value) {
    return 'Konfirmasi password tidak sesuai';
  } else {
    return !!v;
  }
}

const form = ref(false);
const userName = ref("");
const password = ref("");
const passwordConfirmation = ref("");
const userId = ref("");
const formatUserId = () => {
  // Remove spaces and replace with dots
  userId.value = userId.value.replace(/\s+/g, ".");

  // Allow only alphanumeric and dot
  userId.value = userId.value.replace(/[^a-zA-Z0-9.]/g, "");

  // Ensure dots are not added consecutively
  userId.value = userId.value.replace(/\.+/g, ".");
};
const router = useRouter();
const loading = ref(false);
const showSnackbar = ref(false);
const message = ref("");
const isSuccess = ref(false);
const onSubmit = async () => {
  if (!form.value) return;
  loading.value = true;
  const { status } = await useFetch(
    "https://bio-code.cyclic.app/api/v1/auam/register",
    {
      method: "post",
      body: {
        userId: userId.value,
        name: userName.value,
        password: password.value,
      },
    }
  );
  
  if (status.value == 'error') {
    message.value = "User ID telah digunakan";
    isSuccess.value = false;
    showSnackbar.value = true;
  } else {
    message.value = `Hai ${userName.value}, anda telah terdaftar`;
    isSuccess.value = true;
    showSnackbar.value = true;
    setTimeout(() => {
      router.push("/login");
    }, 3000);
  }
  loading.value = false;
};
</script>

<style lang="scss" scoped>
.logo-bg {
  position: absolute;
  width: 859px;
  height: 638px;
  top: 50%;
  left: 50%;

  transform: translate(-50%, -50%);
}
</style>
