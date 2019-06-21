<template>
  <section class="hero is-primary is-fullheight">
    <!-- Hero head: will stick at the top -->
    <div class="hero-head">
      <nav class="navbar">
        <div class="container">
          <div class="navbar-brand">
            <a class="navbar-item">
              <img
                src="../assets/pokemon.png"
                alt="Logo"
              >
            </a>
            <span
              class="navbar-burger burger"
              data-target="navbarMenuHeroA"
            >
              <span></span>
              <span></span>
              <span></span>
            </span>
          </div>
          <div
            id="navbarMenuHeroA"
            class="navbar-menu"
          >
            <div class="navbar-end">
              <a class="navbar-item is-active">
                Home
              </a>
              <router-link
                class="navbar-item"
                to="/documentation"
              >Documentation</router-link>

            </div>
          </div>
        </div>
      </nav>
    </div>

    <!-- Hero content: will be in the middle -->
    <div class="">
      <div class="container has-text-centered">
        <SearchBar />
      </div>
    </div>

    <!-- Hero footer: will stick at the bottom -->
    <div class="hero-foot has-text-centered">
      <nav class="tabs">
        <div class="container">
          <p>Made by laureenpe</p>
        </div>
      </nav>
    </div>
  </section>
</template>

<script>
import SearchBar from ".././components/SearchBar";

export default {
  name: "home",
  components: {
    SearchBar
  }
};
</script>
