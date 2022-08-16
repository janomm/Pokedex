<template>
  <div class="column" is-half is-offset-one-quarter>
    <img src="./assets/pokemon.png">
    <hr>
    <h4 class="is-size-4">Pokedex</h4>
    <input class="input is-rounded" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca">
    <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
    <!-- <div v-for="(poke,index) in resultadoBusca" :key="index"> -->
    <!-- <div v-for="(poke,index) in pokemons" :key="index"> -->
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
      <PokeMonVue :name="poke.name" :url="poke.url" :num="index+1 "/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PokeMonVue from "./components/PokeMonVue";

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(data =>{
      console.log("Pegou a lista de pokemons");
      this.pokemons = data.data.results;
      this.filpokemons = data.data.results;
    })
  },
  components:{
    PokeMonVue
  },
  computed:{
    // resultadoBusca: function(){
    //   if(this.busca.trim().length == 0){
    //     return this.pokemons;
    //   } else {
    //      return this.pokemons.filter(pokemon => pokemon.name == this.busca);
    //   }
    // }
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca.trim().length == 0){
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
      return this.filteredPokemons;
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
#buscaBtn {
  margin-top: 2%;

}
</style>
