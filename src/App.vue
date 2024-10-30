<script  setup >
 import { onMounted, ref, computed } from "vue"
import axios from 'axios';
import Pokemon from './components/Pokemon.vue'

const pokemones = ref([])
const count = ref(0)
const computedPokemons = computed(() => {
    return pokemones.value
})
 onMounted( () => {
  const getPokemons = async () => {

    try {
      const data = await axios.get('https://pokeapi.co/api/v2/pokemon')
      pokemones.value = data.data.results
    } catch (error) {
      console.log(error);
    }
    
  }
  getPokemons()
// const cambiarEstado = nombre => {
    //   const findPokemon = pokemones.value.find(pokemon => pokemon.name === nombre);
    //   if ( !findPokemon ) {
    //     alert(`El nombre "${nombre}" es incorrecto`)
    //     return
    //   }
    //   pokemones.value = pokemones.value.map(pokemon => {
    //     return pokemon.nombre === nombre ? {
    //       ...pokemon,
    //       descubierto: true
    //     } : pokemon
    //   })
    //   console.log(findPokemon);
    // }

 })

</script>

<template>
  <div class=" guess-pokemon">
    <div class="adivinapokemon_logo">
      <img src="./assets/pokemon.webp" width="900 px" alt="pokemon_logo">
    </div>
    <h1 class= "adivinapokemon_title">¿Quien es este Pokemon?</h1>
    <p class= "adivinapokemon_cantidad"> pokemons encontrados: <span> {{ count }} </span></p>
    <div class= "adivinapokemon_grid">
    <Pokemon v-for="pokemon in computedPokemons" :pokemon="pokemon"   key = "pokemon.name"
    @descubrirPokemon=" i => count+=i" />
    </div>
  </div>
</template>

<style scoped>

.adivinapokemon_logo {
  width: 20 rem;
  margin: 0 auto;
}

.adivinapokemon_cantidad {
  font-weight: 900;}
  .adivinapokemon_cantidad span {
    color: palegoldenrod;
    
  }
  .adivinapokemon_grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2rem;
  }

</style>
