<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logoPokemon.png" class="is-half is-offset-one-quarter" id="logo">
      <input type="text" name="" id="" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input is-rounded">
      <br>
      <br>
      <button @click="buscar" class="button is-fullwidth is-link is-rounded"> Buscar </button>
      <br>
      <br>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :number="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';
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
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res =>{
      console.log('Obteve lista de pokemons');
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  methods:{
    buscar: function(){
       this.filteredPokemons = this.pokemons;
       if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
        }
    }
  },
  computed:{
  
  },
  components:{
    Pokemon
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
#logo{
  width: 70%;
}
</style>
