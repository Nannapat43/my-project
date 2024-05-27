<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12" md="8" lg="6">
        <div class="text-center">
          <h1 class="display-1 mb-4">Welcome!</h1>
          <v-btn color="primary" @click="$router.push('/login')">Back to Login</v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<style>
.text-center {
  text-align: center;
}

.mb-4 {
  margin-bottom: 1.5rem;
}
</style>
