<template>
  <div id="app">
    <h1>Hola pokemones</h1>


<table border="1" width="100%">
  <thead>
    <tr>
      <th>Id</th>
      <th>Name</th>
      <th>Height</th>
    </tr>
  </thead>

  <tbody>
    <tr v-for="(pokemon, index ) in pokemonList " :key=index>
      <td>{{pokemon.id}}</td>
      <td> {{pokemon.name}}</td>
      <td> {{pokemon.height}}</td>
    </tr>
  </tbody>
</table>

  </div>
</template>

<script>


export default {
  name: 'App',
 data: function () {
    return {
      pokemonList:[]
    }
  },
  methods:{
    async  fetchPokemones(){
        try{
            const pokemones = await fetch("https://pokeapi.co/api/v2/pokemon?offset=0&limit=100")
            const pokeArray = await pokemones.json()
           pokeArray.results.map(this.fetchPokemon)
        }catch(error){
            console.log(error)
        }
      
    },

    async fetchPokemon(){
        const {url }= arguments[0]
        try{
            const pokemonResponse = await fetch(`${url}`)
            const poke = await pokemonResponse.json()
            console.log(poke)
            this.pokemonList.push(poke)

        }catch(error){
            console.log(error)
        }

    }
  },
  created(){
      this.fetchPokemones()
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
table{
  width: 100%;
  border: 1px solid;
}
</style>
