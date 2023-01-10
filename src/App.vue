
<template>

    <div id="app">  
      
        <img src="./assets/logo.png"> 
        
        <h1 class="is sized-1">Pokedex</h1><br>
        <input class="input is-rounded is-medium" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca">
        <button class="button is-medium is-fullwidth is-dark" id="buscabtn" @click="Buscar">Buscar</button>
        <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
      
  </div>
  
</template>

<script setup>
import axios from 'axios'
import Pokemon from "./components/Pokemon.vue"
</script>
<script>
export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: '',

    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res=> {
      console.log("Lista de pokemons")
      this.pokemons = res.data.results   
      this.filteredPokemons = res.data.results     
    })
  },
  components: {
    Pokemon
  },
  methods: {
    Buscar: function() {
      this.filteredPokemons = this.pokemons
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons
      }else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
  computed: {/*
    resultadoBusca: function() {
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons
      } else {
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }*/
  }
}
</script>

<style scoped>

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
img {
  cursor: pointer;
}
h1 {
  color: rgb(235, 235, 235);
}
#buscabtn {
  margin-top: 2%;
  background-color: #5e5e5e;
}
#buscabtn:hover {
  background-color: #363636;
}

</style>
