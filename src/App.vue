  <template>
    <Error :errorMSG="errorMessage" @clearError="this.errorMessage = '';"/>
    <Nav />
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <div class="w-full h-auto min-h-[400px] bg-yellow-500 bg-opacity-60 p-8 pl-16 pr-16 lg:pr-32 flex justify-between items-center gap-12 flex-col md:flex-row">
      <div class="flex justify-center flex-col w-full">
        <h1 class="text-white text-center text-2xl md:text-3xl font-semibold md:text-left">Leveraging the PokeAPI</h1>
        <h2 class="text-white text-center text-lg md:text- font-light md:text-left mt-4">Get information about Pokemon and Technical Machines easily</h2>
      </div>
      <div class="w-full flex md:justify-end justify-center items-center">
        <img src="./assets/images/pokeball.png" class="motion-safe:animate-spin-slow text-opacity0">
      </div>
    </div>
    <div class="bg-yellow-500 bg-opacity-60 w-full h-[30px]" style="clip-path: polygon(50% 100%, 0 0, 100% 0);"></div>
    <div class="flex items-center justify-center flex-col">
      <div class="md:pl-16 md:pr-16 pl-4 pr-4 mt-16 mb-16 w-full max-w-[1500px]">
        <h1 class="text-3xl font-semibold text-white text-left">Search for Pokemon</h1>
        <div class="flex mt-8 mb-8 w-full max-w-[1400px] md:flex-row flex-col">
          <div class="w-full bg-red-700 h-auto min-h-[200px] mb-4 md:mb-16 rounded-lg rounded-br-none duration-100 max-w-[500px] border-r-red-800 border-r-2">
            <div class="bg-red-800 w-full h-auto min-h-[50px] pt-2 pb-4 rounded-tl-lg rounded-tr-lg" style="clip-path: polygon(30% 0%, 70% 0%, 100% 0, 100% 85%, 68% 85%, 30% 85%, 0 100%, 0 0);">
              <h2 class="text-left text-white w-[90%] ml-[5%] font-semibold">Search Pokemon Name</h2>
              <div class="w-[90%] ml-[5%] flex md:items-center justify-center md:gap-4 md:flex-row flex-col">
                <input v-model="pokeSearched" type="text" class="mt-2 text-left md:w-[70%] w-[100%] left-[5%] rounded-lg bg-neutral-800 p-2 text-white inline-block mb-4" @keydown.enter="getDownEnter()"/>
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
              <div class="flex mt-4 w-[90%] ml-[5%] gap-4">
                <div class="w-full" v-if="this.pokemonEncounterOBJ.length != 0">
                  <h1 class="text-white text-left mb-2 font-semibold">Pokemon Encounter Area(s)</h1>
                  <div class="bg-black rounded-lg h-auto min-h-[30px] p-2 " style="font-family: 'Press Start 2P', cursive;">
                    <div v-for="item in this.pokemonEncounterOBJ">
                      <h1 class="text-neutral-500 text-sm text-left">{{item.location_area.name.replace("-area","")}}</h1>
                    </div>
                  </div>
                </div>
                <div class="w-full" v-if="this.pokemonEncounterOBJ.length != 0">
                  <h1 class="text-white text-left w-full mb-2 font-semibold">Pokemon Encounter Area(s) Codes</h1>
                  <div class="bg-black w-full rounded-lg h-auto min-h-[30px] p-2 " style="font-family: 'Press Start 2P', cursive;">
                    <div class="flex items-start justify-start">
                      <h1 v-for="item in this.pokemonEncounterOBJ" class="text-neutral-500 text-sm text-left inline-block">{{item.location_area.url.replace("https://pokeapi.co/api/v2/location-area/","").replace("/","")}}, </h1>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="w-full flex items-center justify-center">
      <div class="md:pl-16 md:pr-16 pl-4 pr-4 mt-16 mb-16 w-full max-w-[1500px]">
        <h1 class="text-3xl font-semibold text-white text-left">Search an Area Code</h1>
        <div class="bg-neutral-700 p-4 pl-8 pr-8 rounded-lg mt-8 flex gap-4 md:gap-12 md:flex-row flex-col items-center justify-center">
          <div class="md:w-[40%] w-[100%] min-w-[100px]">
      
            <h2 class="text-white mb-4 text-xl font-regular text-center" v-if="!areaSearchData">Input an area code</h2>
            <div class="flex gap-2">
              <input ref="areadigit1" v-model="areadigit1" @keyup="changeAreaCodeFocus(1)" @keyup.space="changeAreaSpace(1)" type="text" maxlength="1" class="rounded-md w-full text-md h-[50px] bg-neutral-900 text-center text-white"/>
              <input ref="areadigit2" v-model="areadigit2" @keyup="changeAreaCodeFocus(2)" @keyup.space="changeAreaSpace(2)" type="text" maxlength="1" class="rounded-md w-full text-md h-[50px] bg-neutral-900 text-center text-white"/>
              <input ref="areadigit3" v-model="areadigit3" @keyup="changeAreaCodeFocus(3)" @keyup.space="changeAreaSpace(3)" type="text" maxlength="1" class="rounded-md w-full text-md h-[50px] bg-neutral-900 text-center text-white"/>
            </div>
            <button v-if="this.areaSearchData" @click="clearAreaFields()" class="bg-yellow-700 text-white rounded-lg pl-4 pr-4 p-2 mt-3 w-full duration-100 hover:bg-yellow-600">Clear Area Code</button>
          </div>
          <div class="w-full bg-neutral-800 bg-opacity-50 rounded-lg p-4" v-if="areaSearchData">
            <h2 class="text-white text-left mb-2"><span class="font-bold mr-2">Area:</span> {{areaSearchData.location.name}} <span>({{(this.areadigit1+this.areadigit2+this.areadigit3).replace(" ","")}})</span></h2>
            <span class="h-[1px] w-full bg-white inline-block bg-opacity-50 rounded-lg mb-2"></span>
            <h2 class="text-white text-left mb-2 font-bold">Pokemon Encounters</h2>
            <div class="flex flex-wrap">
              <h2 v-for="item in areaSearchData.pokemon_encounters" class="text-yellow-500 text-left mr-4">🠊<span class="ml-2 text-white text-opacity-70">{{item.pokemon.name}}</span></h2>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer/>
  </template>

  <script>
  import Nav from './components/Nav.vue'
  import Footer from './components/Footer.vue'
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
        pokemonEncounterOBJ: [],

        areaSearchData: null,

        areadigit1: null,
        areadigit2: null,
        areadigit3: null,
        timesdigit: 0,
        currentNumber: 0,
      }
    },
    components: {
      Nav,
      Error,
      Footer,
    },
    methods:{
      async getDataPokemon(query){
        try{
          let response = await fetch("https://pokeapi.co/api/v2/pokemon/" + this.pokeSearched.toLowerCase())
          this.pokemonOBJ = await response.json()

          let encounters = await fetch('https://pokeapi.co/api/v2/pokemon/' + this.pokeSearched.toLowerCase() + "/encounters")
          this.pokemonEncounterOBJ = await encounters.json()

          console.log(this.pokemonEncounterOBJ)


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

          // console.log(this.pokemonOBJ)
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
      },
      async getLocationInformation(query){

        console.log(query)

        let areaSearch = await fetch('https://pokeapi.co/api/v2/location-area/' + query.replace(" ","") + '/')
        this.areaSearchData = await areaSearch.json()

        console.log(this.areaSearchData)

      },
      changeAreaCodeFocus(number){
        if(number != -1 && number != -2){
          if(number == 1){
            this.timesdigit = 0
            this.$refs.areadigit2.disabled = false
            this.$refs.areadigit2.focus()
            this.$refs.areadigit1.disabled = true
            this.currentNumber = 2
          }else if(number == 2){
            this.timesdigit = 0
            this.$refs.areadigit3.disabled = false
            this.$refs.areadigit3.focus()
            this.$refs.areadigit2.disabled = true
            this.currentNumber = 3
          }else if(number == 3){
            this.timesdigit = 0
            this.$refs.areadigit3.disabled = true
            this.$refs.areadigit3.blur()
            this.getLocationInformation(this.areadigit1.toString()+this.areadigit2.toString()+this.areadigit3.toString())
            console.log("done")
          }
          this.timesdigit++
        }
        console.log(this.timesdigit)
      },
      changeAreaSpace(number){
        if(number == 1){
          this.timesdigit = 0
          this.$refs.areadigit2.disabled = false
          this.$refs.areadigit2.focus()
          this.$refs.areadigit1.disabled = true
          this.currentNumber = 2
        }else if(number == 2){
          this.timesdigit = 0
          this.$refs.areadigit3.disabled = false
          this.$refs.areadigit3.focus()
          this.$refs.areadigit2.disabled = true
          this.currentNumber = 3
        }else if(number == 3){
          this.timesdigit = 0
          this.$refs.areadigit3.disabled = true
          this.$refs.areadigit3.focus()
          this.getLocationInformation(this.areadigit1.toString()+this.areadigit2.toString()+this.areadigit3.toString())
          console.log("done")
        }
      },
      clearAreaFields(){
        this.areaSearchData = null; 
        this.areadigit1 = ''; 
        this.areadigit2 = ''; 
        this.areadigit3 = ''; 
        this.$refs.areadigit1.disabled = false
      },
      getDownEnter(){
        if(this.errorMessage == ""){
          this.getDataPokemon()
        }
      }
    },
    mounted(){
      this.$refs.areadigit2.disabled = true
      this.$refs.areadigit3.disabled = true
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
