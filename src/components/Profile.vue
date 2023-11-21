<template>
  <div>
    {{ currentUser }}
  </div>
</template>

<script>
export default {
  name: "_Profile",
  data() {
    return {};
  },
  computed: {
    currentUser() {
      return JSON.parse(localStorage.getItem("user"));
    },
  },
  mounted() {
    if (!this.currentUser) {
      this.$router.push("/login");
    }
  },
};
</script>