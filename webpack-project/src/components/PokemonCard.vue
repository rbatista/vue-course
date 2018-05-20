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
      let colors = { 3: 'badge-flying', 4: 'badge-poison', 5: 'badge-ground', 6: 'badge-rock', 7: 'badge-bug', 10: 'badge-fire', 11: 'badge-water', 12: 'badge-grass', 13: 'badge-electric', 18: 'badge-fairy' }
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
.badge-normal {
  background: linear-gradient(180deg, #a4acaf 50%, #a4acaf 50%);
  background-color: #a4acaf;
  color: #212121;
}
.badge-fire {
  background: linear-gradient(180deg, #fd7d24 50%, #fd7d24 50%);
  background-color: #fd7d24;
  color: #fff;
}
.badge-water {
  background: linear-gradient(180deg, #4592c4 50%, #4592c4 50%);
  background-color: #4592c4;
  color: #fff;
}
.badge-poison {
    color: #fff;
    background-color: #b97fc9;
}
.badge-flying {
  background: linear-gradient(180deg, #3dc7ef 50%, #bdb9b8 50%);
  background-color: #3dc7ef;
  color: #212121;
}
.badge-rock {
  background: linear-gradient(180deg, #a38c21 50%, #a38c21 50%);
  background-color: #a38c21;
  color: #fff;
}
.badge-ground {
  background-image: linear-gradient(rgb(247, 222, 63) 50%, rgb(171, 152, 66) 50%);
  background-color: #f7de3f;
  color: #212121;
}
.badge-grass {
  background: linear-gradient(180deg, #9bcc50 50%, #9bcc50 50%);
  background-color: #9bcc50;
  color: #212121;
}
.badge-bug {
  background: linear-gradient(180deg, #729f3f 50%, #729f3f 50%);
  background-color: #729f3f;
  color: #fff;
}
.badge-fairy {
  background: linear-gradient(180deg, #fdb9e9 50%, #fdb9e9 50%);
  background-color: #fdb9e9;
  color: #212121;
}
.badge-electric {
  background: linear-gradient(180deg, #eed535 50%, #eed535 50%);
  background-color: #eed535;
   color: #212121;
}
.pokemon-card .card-body .badge {
  margin-left: 2px;
  margin-right: 2px;
}
</style>
