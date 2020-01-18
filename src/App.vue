<template>
  <div id="app">
    <h1>Countries Of The World</h1>
    <h2>Population Of The World: {{worldPopulation}}</h2>
    <country-form :countries="countries"></country-form>

    <div class="container">
      <country-display :country="selectedCountry" :countries="countries"></country-display>
      <img v-if="selectedCountry" class="flag-large":src="selectedCountry.flag" alt="">
      <favourite-countries :countries="favouriteCountries"></favourite-countries>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js'
import CountryForm from './components/countryForm.vue'
import CountryDisplay from './components/countryDisplay.vue'
import FavouriteCountries from './components/favouriteCountries.vue'

export default {
  name: 'app',
  components: {
    "country-form": CountryForm,
    "country-display": CountryDisplay,
    "favourite-countries": FavouriteCountries
  },
  data() {
    return {
      countries: [],
      selectedCountry: null,
      favouriteCountries: []
    }
  },
  computed: {
    worldPopulation: function() {
      return this.populationCalculator(this.countries)
    }
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
      .then(response => response.json())
      .then(objectsArray => this.countries = objectsArray)

    eventBus.$on('country-select', (countryCode) => {
      this.selectedCountry = this.countries.find(country => country.alpha3Code === countryCode)
    })

    eventBus.$on('favourite', (countryCode) => {
      if (this.favouriteCountries.includes(this.countries.find(country => country.alpha3Code === countryCode))) return
      this.favouriteCountries.push(this.countries.find(country => country.alpha3Code === countryCode))
    })

  },
  methods: {
    populationCalculator: function(countries){
        return countries.reduce((runningTotal, country) => runningTotal + country.population, 0);
      }
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
  grid-template-columns: auto auto auto;
  grid-column-gap: 50px;
  text-align: left;
  margin-top: 40px;
}

.flag-large {
  height: 300px;
  /* width: 500px; */
  display: block;
  border: solid 1px;
  text-align: center;
}

.flag-small {
  height: 30px;
  border: solid 1px;
}
</style>
