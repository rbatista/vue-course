<template>
<div>
  <h3>Types</h3>
  <check-filter v-for="type in types" v-bind:key="type.id"
      v-bind:filter-value="type.id" v-bind:filter-name="type.name"
      v-on:check-filter="filterBy">
  </check-filter>
</div>
</template>

<script>
import CheckFilter from './CheckFilter.vue'

export default {
  props: ['types'],
  methods: {
    filterBy: function (typeId, value) {
      this.$emit('filter-by', typeId, value)
    }
  },
  components: {
    CheckFilter
  }
}
</script>
