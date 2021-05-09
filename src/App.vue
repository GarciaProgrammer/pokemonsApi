<template>
  <div id="app">
    <img src="./assets/logo.png" />
    <hr />
    <h4 class="is-size-1">Pokedex</h4>
    <input
      type="text"
      placeholder="Buscar pokemon pelo nome"
      v-model="busca"
      class="input is-rounded column is-half is-offset-one-quarter"
    />
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke, index) in filtrarPokemons" :key="poke.name">
        <Pokemon :nome="poke.name" :num="index" :url="poke.url" />
      </div>
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
      pokemons: [],
      busca: "",
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((dados) => {
        this.pokemons = dados.data.results;
      });
  },
  components: {
    Pokemon,
  },
  computed: {
    filtrarPokemons() {
      if (this.busca == '' || this.busca == ' ') {
        return this.pokemons;  
      } else {
        return this.pokemons.filter(pokemon => pokemon.name.match(this.busca));
        //outra forma
        //return this.pokemons.filter(pokemon => pokemon.name == this.busca);
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

#buttonBuscar {
  margin-top: 7px;
}
</style>
