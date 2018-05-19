<template>
  <div class="row">
    <div v-for="pokemon in pokemons" v-bind:key="pokemon.id" class="col-3">
      <pokemon-card v-bind:pokemon="pokemon"></pokemon-card>
    </div>
  </div>
</template>

<script>
import PokemonCard from './PokemonCard.vue'

export default {
  data () {
    return {
      pokemons: [
        { id: 1, name: 'bulbasaur', types: [ { id: 12, name: 'grass' }, { id: 4, name: 'Poison' } ] },
        { id: 4, name: 'charmander', types: [ { id: 10, name: 'fire' } ] },
        { id: 7, name: 'squardle', types: [ { id: 11, name: 'water' } ] }
      ]
    }
  },
  components: {
    PokemonCard
  }
}
</script>
