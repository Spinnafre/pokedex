<template>
  <div id="#app">
    <h1 class="is-size-1">POKEDEX</h1>
    <div class="column is-half is-offset-one-quarter">
      <div class="control field has-addons">
        <p class="control is-expanded">
          <input class="input" type="text" placeholder="Nome..." v-model="search"/>
        </p>
        <p class="control">
          <a class="button is-primary" @click="searchAction"> Pesquisar </a>
        </p>
      </div>
      <ul>
        <li v-for="(pokemon, i) in newArray" :key="pokemon.name">
          <Pokemon :name="pokemon.name" :url="pokemon.url" :num="i + 1" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";

import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  data() {
    return {
      search: "",
      pokemons: [],
      newArray: [],
    };
  },
  created: function () {
    axios("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(
      (res) => {
        this.pokemons = res.data.results;
        // Para evitar com que altere o array principal uso um clone
        this.newArray=res.data.results
      }
    );
  },
  components: {
    Pokemon,
  },
  methods: {
    searchAction: function () {
      this.newArray=this.pokemons
      if ((this.search === "") | (this.search === " ")) {
        this.newArray=this.pokemons
      }
      else{
        this.newArray=this.pokemons.filter(e=>e.name===this.search)
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
