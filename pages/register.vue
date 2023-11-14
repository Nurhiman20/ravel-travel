<template>
  <v-container fluid class="pa-0 h-screen d-flex container">
    <img class="logo-bg" src="@/assets/images/large-logo.png" alt="logo" />
    <v-card class="ma-auto pa-6 rounded-xl" width="531">
      <h2>Daftar</h2>

      <div class="text-subtitle-1 text-medium-emphasis mt-3">User ID</div>
      <v-text-field
        density="compact"
        variant="outlined"
        placeholder="Masukkan User ID"
        data-cy="input-userId"
      ></v-text-field>

      <div class="text-subtitle-1 text-medium-emphasis mt-1">Nama</div>
      <v-text-field
        density="compact"
        variant="outlined"
        placeholder="Masukkan Nama"
        data-cy="input-name"
      ></v-text-field>

      <div class="text-subtitle-1 text-medium-emphasis mt-1">Password</div>
      <v-text-field
        :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
        :type="visible ? 'text' : 'password'"
        density="compact"
        placeholder="Masukkan password"
        variant="outlined"
        data-cy="input-password"
        @click:append-inner="visible = !visible"
      ></v-text-field>

      <div class="text-subtitle-1 text-medium-emphasis mt-1">Konfirmasi Password</div>
      <v-text-field
        :append-inner-icon="visibleConfirmation ? 'mdi-eye-off' : 'mdi-eye'"
        :type="visibleConfirmation ? 'text' : 'password'"
        density="compact"
        placeholder="Masukkan konfirmasi password"
        variant="outlined"
        data-cy="input-confirmation_password"
        @click:append-inner="visibleConfirmation = !visibleConfirmation"
      ></v-text-field>

      <v-btn block color="primary" size="large" data-cy="btn-register">Daftar</v-btn>
    </v-card>
  </v-container>
</template>

<script setup>
const visible = ref(false);
const visibleConfirmation = ref(false);
</script>

<style lang="scss" scoped>
.container {
  position: relative;
}
.logo-bg {
  position: absolute;
  width: 859px;
  height: 638px;
  top: 50%;
  left: 50%;

  transform: translate(-50%, -50%);
}
</style>
