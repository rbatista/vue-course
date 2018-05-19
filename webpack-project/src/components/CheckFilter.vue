<template>
<div>
  <input type="checkbox" v-bind:id="`check-filter-${filterName}`" v-model="checked" v-on:change="checkFilter"/>
  <label v-bind:for="`check-filter-${filterName}`">{{ filterName }}</label>
</div>
</template>

<script>
export default {
  props: [ 'filter-value', 'filter-name' ],
  data () {
    return {
      checked: false
    }
  },
  methods: {
    checkFilter () {
      this.$emit('check-filter', this.filterValue, this.checked)
    }
  }
}
</script>
