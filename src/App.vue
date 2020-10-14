<template id='template'>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h1>POKEDEX</h1>
      <input
        class="input is-rounded"
        type="text"
        name=""
        id=""
        placeholder="Buscar Pokemon"
        v-model="search"
      />
      <button
        id="searchbtn"
        class="button is-medium is-fullwidth button is-primary is-rounded"
        @click="quest"
      >
        Pesquisar
      </button>

      <hr />
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
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
      filteredPokemons: [],
      search: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    quest() {
      this.filteredPokemons = this.pokemons;
      if (this.search == "" || this.search == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.search
        );
      }
    },
  },
  computed: {
    /*
    result() {
      if (this.search == "" || this.search == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.search);
      }
    },*/
  },
};
</script>

<style>
body {
  background: #b0d5d9;
}
template {
  background: red;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#searchbtn {
  margin-top: 3%;
}
</style>
