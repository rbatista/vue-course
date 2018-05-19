<template>
  <div class="row">
    <div v-for="pokemon in pokemons" v-bind:key="pokemon.id" class="col-3">
      <pokemon-card v-bind:pokemon="pokemon"></pokemon-card>
    </div>
  </div>
</template>

<script>
import PokemonCard from './PokemonCard.vue'
import { pokemons } from '../utils/pokemons.js'

export default {
  data () {
    return {
      pokemons
    }
  },
  components: {
    PokemonCard
  }
}
</script>
