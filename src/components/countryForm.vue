<template lang="html">
  <select v-on:change="handleChange" v-model="selectedCountryCode">
    <option disabled selected>Select a country...</option>
    <option v-for="country in countries" :value="country.alpha3Code">{{country.name}}</option>
  </select>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'country-form',
  props: ['countries'],
  data() {
    return {
      'selectedCountryCode': null
    }
  },
  methods: {
    handleChange(){
      eventBus.$emit('country-select', this.selectedCountryCode)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
