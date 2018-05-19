<template>
  <div class="row">
    <div v-for="pokemon in pokemons" v-bind:key="pokemon.id" class="col-3">
      <pokemon-card v-bind:pokemon="pokemon"></pokemon-card>
    </div>
  </div>
</template>

<script>
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
    'pokemon-card': {
      props: [ 'pokemon' ],
      template: `
        <div class='pokemon-card card'>
          <img v-bind:src="getImage(pokemon.id)" class="card-img-top"/>
          <div class="card-body">
            <h6 class="card-subtitle mb-2 text-muted">#{{ formatId(pokemon.id) }}</h6>
            <h5 class="card-title">{{ pokemon.name | capitalize }}</h5>
            <span class="badge" v-for="type in pokemon.types" v-bind:key="type.id" v-bind:class="getTypeColor(type.id)">{{ type.name }}</span>
          </div>
        </div>
      `,
      methods: {
        getImage: function (id) {
          return 'https://assets.pokemon.com/assets/cms2/img/pokedex/detail/' + this.formatId(id) + '.png'
        },
        formatId: function (id) {
          return String(id).padStart(3, '0')
        },
        getTypeColor: function (typeId) {
          let colors = { 4: 'badge-poison', 10: 'badge-danger', 11: 'badge-primary', 12: 'badge-success' }
          return colors[typeId]
        }
      },
      filters: {
        capitalize: function (str) {
          return (!str || str.lenght === 0) ? '' : str.charAt(0).toUpperCase() + str.slice(1)
        }
      }
    }
  }
}
</script>

<style>
.badge-poison {
    color: #fff;
    background-color: #b97fc9;
}
.pokemon-card .card-body .badge{
  margin-left: 2px;
  margin-right: 2px;
}
</style>
