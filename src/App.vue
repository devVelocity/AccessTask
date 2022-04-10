<template>
  <Error :errorMSG="errorMessage" @clearError="this.errorMessage = '';"/>
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
  <div class="md:pl-16 md:pr-16 pl-4 pr-4 mt-16 mb-24">
    <h1 class="text-3xl font-semibold text-white text-left">Search for Pokemon</h1>
    <div class="flex mt-8 mb-8 w-full max-w-[1400px] md:flex-row flex-col">
      <div class="w-full bg-red-700 h-auto min-h-[200px] mb-4 md:mb-16 rounded-lg rounded-br-none duration-100 max-w-[500px] border-r-red-800 border-r-2">
        <div class="bg-red-800 w-full h-auto min-h-[50px] pt-2 pb-4 rounded-tl-lg rounded-tr-lg" style="clip-path: polygon(30% 0%, 70% 0%, 100% 0, 100% 85%, 68% 85%, 30% 85%, 0 100%, 0 0);">
          <h2 class="text-left text-white w-[90%] ml-[5%] font-semibold">Search Pokemon Name</h2>
          <div class="w-[90%] ml-[5%] flex md:items-center justify-center md:gap-4 md:flex-row flex-col">
            <input v-model="pokeSearched" type="text" class="mt-2 text-left md:w-[70%] w-[100%] left-[5%] rounded-lg bg-neutral-800 p-2 text-white inline-block mb-4"/>
            <button class="md:w-[50%] w-[100%] bg-neutral-700 text-white rounded-lg md:mb-4 mb-8 md:mt-2 p-2 duration-100 hover:bg-neutral-600" @click="getDataPokemon()">Search Pokemon</button>
          </div>
        </div>
        <div class="w-[80%] ml-[10%] mb-8 mt-8 rounded-lg min-h-[200px] h-auto bg-neutral-500 p-4 duration-500">
          <div class="bg-black w-full min-h-[200px] h-auto rounded-lg duration-500">
            <h1 class="text-white pt-4 pb-4 text-lg font-semibold" style="font-family: 'Press Start 2P', cursive;" v-if="pokemonTITLE">{{pokemonTITLE}}</h1>
            <span class="bg-white bg-opacity-50 h-[1px] w-[90%] inline-block mb-4" v-if="this.pokemonTITLE"></span>
            <div>
              <div class="flex justify-between">
                <img :src="this.pokemonIMGOBJ.front" :alt="pokemonTITLE" v-if="this.pokemonIMGOBJ.front" class="w-full">
                <img :src="this.pokemonIMGOBJ.back" :alt="pokemonTITLE" v-if="this.pokemonIMGOBJ.back" class="w-full">
              </div>
              <div class="flex justify-between mt-4">
                <img :src="this.pokemonIMGOBJ.front_shiny" :alt="pokemonTITLE" v-if="this.pokemonIMGOBJ.front_shiny" class="w-full">
                <img :src="this.pokemonIMGOBJ.back_shiny" :alt="pokemonTITLE" v-if="this.pokemonIMGOBJ.back_shiny" class="w-full">
              </div>
            </div>
            <span class="bg-white bg-opacity-50 h-[1px] w-[90%] inline-block mb-4 mt-4" v-if="this.pokemonTITLE"></span>
          </div>
        </div>
        <div class="w-[90%] ml-[5%] h-auto min-h-[30px] mb-4">
        </div>

      </div>
      <div class="w-full bg-red-700 h-auto min-h-[200px] mt-4 md:mt-16 pb-8 rounded-lg rounded-tl-none pt-32  duration-100" style="clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 100%, 70% 100%, 30% 100%, 0 100%, 0 0);">
        <div class="mr-24 w-[70%] md:w-[85%] md:max-w-[650px] mb-8">
          <!-- <h1 class="text-white text-left w-[90%] ml-[5%] mb-2 font-semibold">Pokemon Description</h1>
          <div class="bg-black w-[90%] ml-[5%] rounded-lg h-auto min-h-[30px] p-4">
            <h1 class="text-white">{{pokemonDESC}}</h1>
          </div> -->
          <div class="flex w-[90%] ml-[5%] mt-2 gap-4">
            <div class="w-full">
              <h1 class="text-white text-left w-full mb-2 font-semibold">Height</h1>
              <div class="bg-black w-full rounded-lg h-auto min-h-[30px] p-2 " style="font-family: 'Press Start 2P', cursive;">
                <h1 class="text-white">{{pokemonHEIGHT}}</h1>
              </div>
            </div>
            <div class="w-full">
              <h1 class="text-white text-left w-full mb-2 font-semibold">Weight</h1>
              <div class="bg-black w-full rounded-lg h-auto min-h-[30px] p-2 " style="font-family: 'Press Start 2P', cursive;">
                <h1 class="text-white">{{pokemonWEIGHT}}</h1>
              </div>
            </div>
            
          </div>
          <div class="mt-4">
            <h1 class="text-white text-left w-[90%] ml-[5%] mb-2 font-semibold">Base Experience</h1>
            <div class="bg-black w-[44%] ml-[5%] rounded-lg h-auto min-h-[30px] p-2 " style="font-family: 'Press Start 2P', cursive;">
                <h1 class="text-white text-sm text-center">{{this.pokemonOBJ.base_experience}}</h1>
            </div>
          </div>
          <div class="mt-4">
            <h1 class="text-white text-left w-[90%] ml-[5%] mb-2 font-semibold">Pokemon Stats</h1>
            <div class="bg-black w-[90%] ml-[5%] rounded-lg h-auto min-h-[30px] p-2 " style="font-family: 'Press Start 2P', cursive;">
              <div v-for="item in this.pokemonOBJ.stats">
                <h1 class="text-neutral-500 text-sm text-left">{{item.stat.name}}: <span class="ml-1 text-white">{{item.base_stat}}</span></h1>
              </div>
            </div>
          </div>
          <div class="mt-4">
            <h1 class="text-white text-left w-[90%] ml-[5%] mb-2 font-semibold">Pokemon Types</h1>
            <div class="bg-black w-[90%] ml-[5%] rounded-lg h-auto min-h-[30px] p-2 " style="font-family: 'Press Start 2P', cursive;">
              <div v-for="item in this.pokemonOBJ.types">
                <h1 class="text-neutral-500 text-sm text-left">{{item.type.name}}</h1>
              </div>
            </div>
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
      pokemonOBJ: {},
      errorMessage: "",

      pokeSearched: null,

      pokemonDESC: null,
      pokemonFULLTITLE: null,
      pokemonTITLEFirst: null,
      pokemonTITLE: null,
      pokemonHEIGHT: null,
      pokemonWEIGHT: null,

      pokemonIMG: null,
      pokemonIMGShiny: null,

      pokemonIMGToggle: null,

      pokemonIMGOBJ: {"front":null,"back":null,"front_shiny":null,"back_shiny":null},
    }
  },
  components: {
    Nav,
    Error,
  },
  methods:{
    async getDataPokemon(query){
      try{
        let response = await fetch("https://pokeapi.co/api/v2/pokemon/" + this.pokeSearched.toLowerCase())
        this.pokemonOBJ = await response.json()

        this.pokemonFULLTITLE = this.pokemonOBJ.species.name
        this.pokemonTITLEFirst = this.pokemonOBJ.species.name.charAt(0).toUpperCase()
        this.pokemonTITLE = this.pokemonTITLEFirst + this.pokemonFULLTITLE.slice(1)

        this.pokemonIMGOBJ.front = this.pokemonOBJ.sprites.front_default
        this.pokemonIMGOBJ.back = this.pokemonOBJ.sprites.back_default
        this.pokemonIMGOBJ.front_shiny = this.pokemonOBJ.sprites.front_shiny
        this.pokemonIMGOBJ.back_shiny = this.pokemonOBJ.sprites.back_shiny

        this.pokemonHEIGHT = this.pokemonOBJ.height
        this.pokemonWEIGHT = this.pokemonOBJ.weight
        
        // this.pokemonDESC = this.pokemonOBJ.

        this.pokeSearched = ""

        console.log(this.pokemonOBJ)
      }catch(error){
        this.pokemonOBJ = {}
        this.pokemonIMGOBJ = {}
        this.pokemonTITLE = ""
        this.pokemonHEIGHT = ""
        this.pokemonWEIGHT = ""
        if(error.message = "JSON.parse: unexpected character at line 1 column 1 of the JSON data"){
          this.errorMessage = "Pokemon not found"
        }else{
          this.errorMessage = error.message
        }
        // console.log(this.errorMessage)
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
