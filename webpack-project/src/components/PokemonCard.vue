<template>
<div class='pokemon-card card'>
  <img v-bind:src="getImage(pokemon.id)" class="card-img-top"/>
  <div class="card-body">
    <h6 class="card-subtitle mb-2 text-muted">#{{ formatId(pokemon.id) }}</h6>
    <h5 class="card-title">{{ pokemon.name | capitalize }}</h5>
    <span class="badge" v-for="type in pokemon.types" v-bind:key="type" v-bind:class="getTypeColor(type)">{{ getTypeById(type).name }}</span>
  </div>
</div>
</template>

<script>
import { types } from '../utils/pokemons.js'

export default {
  props: [ 'pokemon' ],

  methods: {
    getImage: function (id) {
      return require(`../assets/pokemons/${this.formatId(id)}.png`)
    },
    formatId: function (id) {
      return String(id).padStart(3, '0')
    },
    getTypeById: function (typeId) {
      let type = types.find((elem, indx, array) => elem.id === typeId)
      return type !== undefined ? type : {}
    },
    getTypeColor: function (typeId) {
      let colors = { 3: 'badge-flying', 4: 'badge-poison', 7: 'badge-success', 10: 'badge-danger', 11: 'badge-primary', 12: 'badge-success' }
      return colors[typeId] || 'badge-secondary'
    }
  },

  filters: {
    capitalize: function (str) {
      return (!str || str.lenght === 0) ? '' : str.charAt(0).toUpperCase() + str.slice(1)
    }
  }
}
</script>

<style>
.badge-poison {
    color: #fff;
    background-color: #b97fc9;
}
.badge-flying {
  background: linear-gradient(180deg, #3dc7ef 50%, #bdb9b8 50%);
  background-color: #3dc7ef;
  color: #212121;
}
.pokemon-card .card-body .badge {
  margin-left: 2px;
  margin-right: 2px;
}
</style>
