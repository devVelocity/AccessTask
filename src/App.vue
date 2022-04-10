<template>
  <Error :errorMSG="errorMessage"/>
  <Nav />
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <div class="w-full h-auto min-h-[400px] bg-yellow-500 bg-opacity-60 p-8 flex justify-between items-center">
    <div class="flex justify-center flex-col">
      <h1 class="text-white text-2xl md:text-3xl font-semibold text-left">Leveraging the PokeAPI</h1>
      <h2 class="text-white text-lg md:text- font-light text-left mt-4">Get information about Pokemon, Pokemon Forms, etc...</h2>
    </div>
    <div>

    </div>
  </div>
</template>

<script>
import Nav from './components/Nav.vue'
import Error from './components/Error.vue'

export default {
  name: 'App',
  data(){
    return{
      pokemonOBJ: null,
      errorMessage: "",
    }
  },
  components: {
    Nav,
    Error,
  },
  methods:{
    async getDataPokemon(query){
      try{
        let response = await fetch("https://pokeapi.co/api/v2/pokemon/" + query)
        this.pokemonOBJ = await response.json()
      }catch(error){

      }
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
</style>
