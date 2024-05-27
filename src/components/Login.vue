<template>
  <v-container class="fill-height background" fluid>
    <v-row class="fill-height" align="center" justify="center">
      <v-col cols="12" md="6" lg="4">
        <v-card class="card-background mt-4 mb-8">
          <v-card-text>
            <v-card-title>
              <span class="headline text-white" style="font-size: 30px"
                >Sign In</span
              >
            </v-card-title>
            <v-form ref="form" v-model="valid" @submit.prevent="submit">
              <v-col>
                <v-text-field
                  v-model="emailOrPhone"
                  :rules="emailOrPhoneRules"
                  placeholder="Email or phone number"
                  class="text-white"
                  variant="outlined"
                  required
                ></v-text-field>
              </v-col>
              <v-col>
                <v-text-field
                  v-model="password"
                  :rules="passwordRules"
                  :append-inner-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                  :type="showPassword ? 'text' : 'password'"
                  placeholder="Password"
                  class="text-white"
                  variant="outlined"
                  @click:append-inner="showPassword = !showPassword"
                  required
                ></v-text-field>
              </v-col>
              <v-col class="d-flex justify-center">
                <v-btn
                  :loading="loading"
                  color="red"
                  class="mt-2"
                  text="Sign In"
                  type="submit"
                  size="large"
                  block
                  :disabled="!valid"
                ></v-btn>
              </v-col>
              <v-row class="d-flex inline justify-space-between">
                <v-col cols="auto">
                  <v-checkbox
                    v-model="rememberMe"
                    label="Remember Me"
                    class="text-white text-caption"
                  ></v-checkbox>
                </v-col>
                <v-col cols="auto">
                  <v-card-title class="text-end">
                    <span
                      class="headline text-white"
                      style="
                        font-size: 1rem;
                        color: rgba(255, 255, 255, 0.7);
                        cursor: pointer;
                      "
                      >Need help?</span
                    >
                  </v-card-title>
                </v-col>
              </v-row>
              <v-col>
                <v-col>
                  <span
                    style="
                      margin-block-start: 0;
                      margin-block-end: 0;
                      margin: 0;
                      padding: 0;
                      color: rgba(255, 255, 255, 0.7);
                      font-size: 1rem;
                      font-weight: 400;
                      margin-top: 16px;
                    "
                    >New to Netflix?
                    <span
                      @click="signup()"
                      rel="noopener noreferrer"
                      target="_blank"
                      style="
                        color: rgb(255, 255, 255);
                        font-weight: 500;
                        cursor: pointer;
                      "
                      >Sign up now</span
                    >
                  </span>
                </v-col>
              </v-col>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      valid: false,
      rememberMe: false,
      emailOrPhone: "",
      password: "",
      showPassword: false,
      loading: false,
      emailOrPhoneRules: [
        (v) => !!v || "Please enter a valid email or phone number.",
        (v) =>
          /.+@.+\..+/.test(v) ||
          /^\d{10}$/.test(v) ||
          "Email must be valid or Phone Number",
      ],
      passwordRules: [
        (v) =>
          v.length >= 4 ||
          "Your password must contain between 4 and 60 characters.",
      ],
    };
  },
  methods: {
    async submit() {
      if (this.$refs.form.validate()) {
        this.loading = true;
        try {
          const response = await axios.post("http://localhost:3000/api/login", {
            emailOrPhone: this.emailOrPhone,
            password: this.password,
          });
          this.$router.push("/welcome");
          alert(response.data.message);
        } catch (error) {
          if (error.response) {
            alert(error.response.data.message);
          } else {
            alert("An error occurred. Please try again.");
          }
        } finally {
          this.loading = false;
        }
      }
    },
    signup() {

    },
  },
};
</script>

<style scoped>
.fill-height {
  min-height: 100vh;
  position: relative;
  overflow: hidden;
}

.background {
  background-image: url("@/assets/moviepic.jpg");
  background-size: cover;
  background-position: center;
  position: fixed;
  width: 100%;
  height: 100%;
  z-index: 2;
}

.background-blur {
  position: fixed;
  width: 100%;
  height: 100%;
  backdrop-filter: blur(8px);
  z-index: -2;
}

.card-background {
  min-height: 707px;
  padding: 48px 16px;
  border-radius: 10px;
  background-color: rgba(0, 0, 0, 0.7);
  box-sizing: border-box;
  flex-direction: column;
  margin: 0;
}

.input-border {
  background-color: light-dark(
    rgb(232, 240, 254),
    rgba(70, 90, 126, 0.4)
  ) !important;
  color: fieldtext !important;
}
</style>
