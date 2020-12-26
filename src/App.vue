<template>
  <div id="app">

  <div class="column is-half is-offset-one-quarter">
    <img src="./assets/pokemon.png" alt="">
    <hr>
    <h4 class="is-size-4">POKEDEX</h4>
    <input class="input is-rounded" type="text"  placeholder="Buscar pokémon pelo nome" v-model="busca">
   <button class="button is-medium is-fullwidth is-success" id="btn" @click="buscar()">Buscar</button>
    <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
    <pokemon :name="poke.name" :url="poke.url" :num="index+1" />
  </div>
    
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import pokemon from "./components/pokemon"

export default {
  name: 'App',
  components: {
   pokemon
  },
  data(){
    return{
      pokemons:[],
      filteredPokemons:[],
      busca:''
      }
  },
   computed:{
  //   resultadoBusca: function(){
  //     if(this.busca == '' || this.busca == ' '){
  //       return this.pokemons
  //   }else{
  //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)
  //   }
  // }
  },
  created(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a Lista de Pkemóns")
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results

    })
  },
  methods:{
    buscar(){
      this.filteredPokemons = this.pokemons
          if(this.busca == '' || this.busca == ' '){
            this.filteredPokemons = this.pokemons;
          }else{
            this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
          }
          console.log("Buscar")
      
    }
  }
}
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
#btn {
  margin-top: 3%;
}
</style>
