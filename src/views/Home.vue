<template>
  <section class="hero is-primary is-fullheight">
    <!-- Hero head: will stick at the top -->
    <div class="hero-head">
      <nav class="navbar">
        <div class="container">
          <div class="navbar-brand">
            <a class="navbar-item">

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
            v-for="item in pokemons"
            :key="item.id"
          >

            <div class="card">
              <div class="additional">
                <div class="user-card">
                  <div class="points">
                    {{item.name}}
                  </div>
                  <figure class="image is-128x128 is-centered">
                    <img
                      :src="item.sprites.back_default"
                      class="is-rounded"
                    >
                  </figure>

                </div>
                <div class="more-info">
                  <h1> {{item.name}}</h1>
                  <div class="coords">
                    <p>Description: {{item.description}}</p>
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
import SearchBar from "../components/SearchBar";
//import Card from ".././components/Cards";
import axios from "axios";
import Axios from "axios";
import { log } from "util";
import { async } from "q";

var pokemonApi = "https://pokeapi.co/api/v2/pokemon/";
var pokemonCharacteristics = "https://pokeapi.co/api/v2/characteristic/";

export default {
  components: {
    SearchBar
  },
  data() {
    return {
      pokemons: []
    };
  },
  methods: {
    async getPokemonsByName(name) {
      let getName = await axios.get(pokemonApi + name);
      return getName;
    }
  },
  async mounted() {
    let pokemons = await axios.get(pokemonApi);
    let results = pokemons.data.results;

    //iterate in results
    for (let index = 0; index < results.length; index++) {
      const element = results[index];
      const result = await this.getPokemonsByName(element.name);
      let pokemon = result.data;

      //Url Id pokemon
      const pokemonId = pokemon.id;
      const urlPokemon = await axios.get(pokemonCharacteristics + pokemonId);
      const getData = urlPokemon.data;

      const getDescriptions = getData.descriptions;
      console.log("getDescription ", getDescriptions);

      pokemon.description = getDescriptions[0].description;
      this.pokemons.push(pokemon);
      //console.log("array", this.description);
    }
  }
};
</script>
