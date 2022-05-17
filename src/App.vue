<template>

  <div id="app">
   
    <div class="column is-half is-offset-one-quarter">
       <img src="./assets/pokemon-256.png"> 
       <h3 class="is-size-5">POKEDEX:</h3>

      <input type="text" class="input is-rounded" name="" id="" placeholder="Buscar Pokemon por nome:" v-model="busca">
      <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokenons" :key="poke.url" >
        <Pkm :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
      
 
  </div>
</template>

<script> 
import axios from 'axios';
import Pkm from './components/Pokemon-List'; 

export default {
  name: 'App',
  data(){
    return {
      pokemons : [],
      filteredPokenons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
        console.log("Pegou a lista de pokemons")
        this.pokemons = res.data.results; 
        this.filteredPokenons = res.data.results; 
    })
  },
  components: {
    Pkm 
  },
  methods:{
    buscar: function(){
            this.filteredPokenons = this.pokemons;
            if(this.busca == '' || this.busca == ' '){ 
              this.filteredPokenons = this.pokemons;
           }else{ 
              this.filteredPokenons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  },
  computed:{
    // resultadoBusca: function(){
    //   if(this.busca == '' || this.busca == ' '){
    //     return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca);
    //   }
    // }
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
