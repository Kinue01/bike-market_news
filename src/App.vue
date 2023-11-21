<template>
  <div>
    <nav class="navbar border-bottom navbar-expand-lg bg-white">
      <div class="container-fluid">
        <a class="navbar-brand" href="/">Веломаркет</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link to="/" class="nav-link">Home</router-link>
            </li>
          </ul>
          <div v-if="!currentUser">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item">
                <router-link to="/registration" class="nav-link"
                  >Sign Up</router-link
                >
              </li>
              <li class="nav-item">
                <router-link to="/login" class="nav-link">Login</router-link>
              </li>
            </ul>
          </div>
          <div v-if="currentUser">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item">
                <router-link to="/profile" class="nav-link">{{
                  currentUser.username
                }}</router-link>
              </li>
              <li class="nav-item">
                <a class="nav-link" @click.prevent="logOut">LogOut</a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </nav>

    <div class="container">
      <router-view />
    </div>
  </div>
  <Footer class="fixed-bottom"></Footer>
</template>

<script>
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Footer,
  },
  data() {},
  computed: {
    currentUser() {
      return JSON.parse(localStorage.getItem("user"));
    },
  },
  methods: {
    logOut() {
      localStorage.removeItem("user");
      this.$router.push("/login");
    },
  },
};
</script>

