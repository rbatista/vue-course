<template>
  <div class="row">
    <div class="col-10">
      <div class="row">
        <div v-for="pokemon in filteredPokemons" v-bind:key="pokemon.id" class="col-3">
          <pokemon-card v-bind:pokemon="pokemon"></pokemon-card>
        </div>
      </div>
    </div>
    <div class="col-2">
      <type-filter v-bind:types="types" v-on:filter-by="filterType"></type-filter>
    </div>
  </div>
</template>

<script>
import PokemonCard from './PokemonCard.vue'
import TypeFilter from './TypeFilter.vue'
import { pokemons, types } from '../utils/pokemons.js'

export default {
  data () {
    return {
      pokemons,
      types,
      typeFilter: []
    }
  },
  methods: {
    filterType: function (typeId, value) {
      if (value) {
        this.typeFilter.push(typeId)
      } else {
        let index = this.typeFilter.indexOf(typeId)
        if (index >= 0) this.typeFilter.splice(index, 1)
      }
    },
    pokemonPassTypeFilter (pokemon) {
      return !this.typeFilter.length ||
        this.typeFilter.filter(type =>
          pokemon.types.indexOf(type) !== -1
        ).length === this.typeFilter.length
    }
  },
  computed: {
    filteredPokemons () {
      return this.pokemons.filter(this.pokemonPassTypeFilter)
    }
  },
  components: {
    PokemonCard,
    TypeFilter
  }
}
</script>
