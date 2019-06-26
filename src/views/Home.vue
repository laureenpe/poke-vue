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
    <div>
      <div class="container has-text-centered">
        <SearchBar />
        <div class="columns is-multiline is-1-mobile">
          <div
            class="column pa-4"
            v-for="item in data"
            :key="item.id"
          >
            <div class="card">
              <div class="additional">
                <div class="user-card">
                  <div class="points">
                    {{ item.name }}
                  </div>
                  <figure class="image is-128x128">
                    <img :src="item.sprites.back_default">
                  </figure>

                </div>
                <div class="more-info">
                  <h1>Jane Doe</h1>
                  <div class="coords">
                    <span>Group Name</span>
                    <span>Joined January 2019</span>
                  </div>
                  <div class="coords">
                    <span>Position/Role</span>
                    <span>City, Country</span>
                  </div>

                </div>
              </div>
            </div>
          </div>
        </div>
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
//import Card from ".././components/Cards";
import axios from "axios";
let urlApi = "https://pokeapi.co/api/v2/pokemon/";

export default {
  name: "home",
  components: {
    SearchBar
    //Card
  },
  data() {
    return {
      data: []
    };
  },
  methods: {
    async getPokemonById(id) {
      let pokemon = await axios.get(urlApi + id);
      return pokemon;
    }
  },
  async mounted() {
    let pokemons = await axios.get(urlApi);
    console.log(pokemons.data);
    let results = pokemons.data.results;
    for (let index = 0; index < results.length; index++) {
      const element = results[index];
      const pokemon = await this.getPokemonById(element.name);
      this.data.push(pokemon.data);
    }
  }
};
</script>
