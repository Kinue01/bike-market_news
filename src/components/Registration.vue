<template>
  <div class="container bg-white mt-5">
    <form @submit="handleRegister" :validation-schema="schema">
      <div v-if="!successful">
        <div class="mt-3">
          <label for="username" class="form-label">Username</label>
          <input
            type="text"
            name="username"
            class="form-control"
            v-model="username"
          />
          <label name="username" class="error-feedback" />
        </div>
        <div class="mt-3">
          <label for="email" class="form-label">Email</label>
          <input
            name="email"
            type="email"
            class="form-control"
            v-model="email"
          />
          <label name="email" class="error-feedback" />
        </div>
        <div class="mt-3">
          <label for="password" class="form-label">Password</label>
          <input
            name="password"
            type="password"
            class="form-control"
            v-model="password"
          />
          <label name="password" class="error-feedback" />
        </div>

        <div class="mt-3">
          <button class="btn btn-primary btn-block" :disabled="loading">
            <span
              v-show="loading"
              class="spinner-border spinner-border-sm"
            ></span>
            Sign Up
          </button>
        </div>
      </div>
    </form>
    <div
      v-if="message"
      class="alert mt-3"
      :class="successful ? 'alert-success' : 'alert-danger'"
    >
      {{ message }}
    </div>
  </div>
</template>

<script>
import * as yup from "yup";

export default {
  name: "_Registration",
  data() {
    const schema = yup.object().shape({
      username: yup
        .string()
        .required("Username is required!")
        .min(3, "Must be at least 3 characters!")
        .max(20, "Must be maximum 20 characters!"),
      email: yup
        .string()
        .required("Email is required!")
        .email("Email is invalid!")
        .max(50, "Must be maximum 50 characters!"),
      password: yup
        .string()
        .required("Password is required!")
        .min(6, "Must be at least 6 characters!")
        .max(40, "Must be maximum 40 characters!"),
    });
    return {
      username: "",
      password: "",
      email: "",
      successful: false,
      loading: false,
      message: "",
      schema,
    };
  },
  computed: {
    loggedIn() {
      return JSON.parse(localStorage.getItem("user"));
    },
  },
  mounted() {
    if (this.loggedIn) {
      this.$router.push("/profile");
    }
  },
  methods: {
    handleRegister() {
      this.message = "";
      this.successful = false;
      this.loading = true;

      var user = {
        username: this.username,
        email: this.email,
        password: this.password,
      };

      localStorage.setItem("user", JSON.stringify(user));

      this.successful = true;
      this.loading = false;
    },
  },
};
</script>