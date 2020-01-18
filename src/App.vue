<template>
  <div id="app">
    <h1>Countries Of The World</h1>
    <country-form :countries="countries"></country-form>

    <div class="container">
      <country-display :country="selectedCountry"></country-display>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js'
import CountryForm from './components/countryForm.vue'
import CountryDisplay from './components/countryDisplay.vue'

export default {
  name: 'app',
  components: {
    "country-form": CountryForm,
    "country-display": CountryDisplay
  },
  data() {
    return {
      countries: [],
      selectedCountry: null
    }
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
      .then(response => response.json())
      .then(objectsArray => this.countries = objectsArray)

    eventBus.$on('country-select', (country) => {
      this.selectedCountry = country
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  text-align: center;
}

h1 {
}

.container {
  display: grid;
  grid-template-columns: auto auto;
  grid-column-gap: 300px;
  text-align: left;
  margin-top: 40px;
}
</style>
