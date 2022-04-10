<template>
  <Error :errorMSG="errorMessage"/>
  <Nav />
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <div class="w-full h-auto min-h-[400px] bg-yellow-500 bg-opacity-60 p-8 pl-16 pr-16 lg:pr-32 flex justify-between items-center gap-12 flex-col md:flex-row">
    <div class="flex justify-center flex-col w-full">
      <h1 class="text-white text-center text-2xl md:text-3xl font-semibold md:text-left">Leveraging the PokeAPI</h1>
      <h2 class="text-white text-center text-lg md:text- font-light md:text-left mt-4">Get information about Pokemon, Pokemon Forms, etc...</h2>
    </div>
    <div class="w-full flex md:justify-end justify-center items-center">
      <img src="./assets/images/pokeball.png" class="motion-safe:animate-spin-slow text-opacity0">
    </div>
  </div>
  <div class="bg-yellow-500 bg-opacity-60 w-full h-[30px]" style="clip-path: polygon(50% 100%, 0 0, 100% 0);"></div>
  <div class="pl-16 pr-16 mt-16">
    <h1 class="text-3xl font-semibold text-white text-left">Search for Pokemon</h1>
    <div class="flex mt-8 mb-8 w-full max-w-[1400px] md:flex-row flex-col">
      <div class="w-full bg-red-700 h-auto min-h-[200px] mb-4 md:mb-16 rounded-lg rounded-br-none duration-100">
        <div class="bg-red-800 w-full h-auto min-h-[50px] pt-2 pb-4 rounded-tl-lg rounded-tr-lg" style="clip-path: polygon(30% 0%, 70% 0%, 100% 0, 100% 85%, 68% 85%, 30% 85%, 0 100%, 0 0);">
          <h2 class="text-left text-white w-[90%] ml-[5%] font-semibold">Search Pokemon Name</h2>
          <div class="w-[90%] ml-[5%] flex items-center justify-center md:gap-4 md:flex-row flex-col">
            <input type="text" class="mt-2 text-left md:w-[70%] w-[90%] left-[5%] rounded-lg bg-neutral-800 p-2 text-white inline-block mb-4"/>
            <button class="md:w-[50%] w-[90%] bg-neutral-700 text-white rounded-lg md:mb-4 mb-8 md:mt-2 p-2 duration-100 hover:bg-neutral-600">Search Pokemon</button>
          </div>
        </div>
        <div class="w-[80%] ml-[10%] mb-8 mt-8 rounded-lg min-h-[200px] h-auto bg-neutral-500 p-4">
          <div class="bg-black w-full min-h-[200px] h-auto rounded-lg">
            <h1 class="text-white pt-4 pb-4">rawr {{pokemonTITLE}}</h1>
            <span class="bg-white bg-opacity-50 h-[1px] w-[90%] ml-[5%] block"></span>
            <img :src="pokemonIMG" :alt="pokemonTITLE">
          </div>
        </div>
        <div class="w-[90%] ml-[5%] h-auto min-h-[30px] mb-4">
        </div>

      </div>
      <div class="w-full bg-red-700 h-auto min-h-[200px] mt-4 md:mt-16 pb-8 rounded-lg rounded-tl-none pt-32  duration-100" style="clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 100%, 70% 100%, 30% 100%, 0 100%, 0 0);">
        <h1 class="text-white text-left w-[90%] ml-[5%] mb-2 font-semibold">Pokemon Description</h1>
        <div class="bg-black w-[90%] ml-[5%] rounded-lg h-auto min-h-[30px] p-4">
          <h1 class="text-white">{{pokemonDESC}}</h1>
        </div>
        <div class="flex w-[90%] ml-[5%] mt-4 gap-12">
          <div class="w-full">
            <h1 class="text-white text-left w-full mb-2 font-semibold">Height</h1>
            <div class="bg-black w-full rounded-lg h-auto min-h-[30px] p-4">
              <h1 class="text-white">{{pokemonHEIGHT}}</h1>
            </div>
          </div>
          <div class="w-full">
            <h1 class="text-white text-left w-full mb-2 font-semibold">Weight</h1>
            <div class="bg-black w-full rounded-lg h-auto min-h-[30px] p-4">
              <h1 class="text-white">{{pokemonWEIGHT}}</h1>
            </div>
          </div>
        </div>
        <div class="mt-4">
          <h1 class="text-white text-left w-[90%] ml-[5%] mb-2 font-semibold">Pokemon Abilities</h1>
          <div class="bg-black w-[90%] ml-[5%] rounded-lg h-auto min-h-[30px] p-4">
            <h1 class="text-white">{{pokemonDESC}}</h1>
          </div>
        </div>
      </div>
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

      pokemonDESC: null,
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
