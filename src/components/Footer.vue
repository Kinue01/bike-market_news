<template>
  <div class="bg-white">
    <footer
      class="row row-cols-1 row-cols-sm-2 row-cols-md-5 py-5 my-5 border-top"
    >
      <div class="col mb-3">
        <p class="text-body-secondary">© 2023</p>
      </div>
      <div class="col mb-3">
        <h5>Section</h5>
        <ul class="nav flex-column">
          <li class="nav-item mb-2">
            <router-link to="/home" class="nav-link p-0 text-body-secondary"
              >Home</router-link
            >
          </li>
        </ul>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: "_Footer",
};
</script>