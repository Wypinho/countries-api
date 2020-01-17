<template lang="html">
  <select v-on:change="handleChange" v-model="selectedCountry">
    <option v-for="country in countries" :value="country">{{country.name}}</option>
  </select>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'country-form',
  props: ['countries'],
  data() {
    return {
      'selectedCountry': {}
    }
  },
  methods: {
    handleChange(){
      eventBus.$emit('country-select', this.selectedCountry)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
