<template>
  <v-container fluid class="pa-0 h-screen">
    <v-row no-gutters>
      <v-col cols="12" md="6">
        <v-img src="@/assets/images/login-image.png" cover :max-height="'100vh'"></v-img>
      </v-col>
      <v-col cols="12" md="6">
        <v-card class="ma-9 pa-6 d-flex flex-column">
          <div class="d-flex flex-row align-center mx-auto">
            <img class="logo" src="@/assets/images/logo.png" alt="">
            <div class="d-flex flex-column ml-1">
              <p class="text-h2 font-weight-bold">Ravel</p>
              <p class="text-caption">Travel Solution by Randy</p>
            </div>
          </div>
          <div class="d-flex flex-column mt-6">
            <h2>Masuk</h2>

            <div class="text-subtitle-1 text-medium-emphasis mt-3">User ID</div>
            <v-text-field
              density="compact"
              variant="outlined"
            ></v-text-field>
            
            <div class="text-subtitle-1 text-medium-emphasis mt-1">Password</div>
            <v-text-field
              density="compact"
              variant="outlined"
              type="password"
            ></v-text-field>

            <v-checkbox label="Ingat saya"></v-checkbox>

            <v-btn
              block
              color="primary"
              size="large"
            >
              Log In
            </v-btn>

            <p class="mx-auto font-weight-medium mt-3">atau</p>

            <p class="mx-auto font-weight-medium mt-3">Belum punya akun? <span class="text-primary pointer">Daftar</span></p>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

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
