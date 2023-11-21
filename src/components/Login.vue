<template>
  <div class="container bg-white mt-5">
    <form @submit="handleLogin" :validation-schema="schema">
      <div class="mt-3">
        <label for="username" class="form-label">Username</label>
        <input name="username" type="text" class="form-control" />
        <label name="username" class="error-feedback" />
      </div>
      <div class="mt-3">
        <label for="password" class="form-label">Password</label>
        <input name="password" type="password" class="form-control" />
        <label name="password" class="error-feedback" />
      </div>

      <div class="mt-3">
        <button class="btn btn-primary btn-block" :disabled="loading">
          <span
            v-show="loading"
            class="spinner-border spinner-border-sm"
          ></span>
          <span>Login</span>
        </button>
      </div>

      <div class="mt-3">
        <div v-if="message" role="alert" class="alert alert-danger">
          {{ message }}
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import * as yup from "yup";

export default {
  name: "_Login",
  data() {
    const schema = yup.object().shape({
      username: yup.string().required("Username is required!"),
      password: yup.string().required("Password is required!"),
    });
    return {
      loading: false,
      message: "",
      schema,
    };
  },
  methods: {
    handleLogin() {
      this.loading = true;

      var user = JSON.parse(localStorage.getItem("user"));

      if (user != null) {
        this.$router.push("/profile");
        this.loading = false;
      } else {
        this.message = "Не получилось";
      }
    },
  },
};
</script>