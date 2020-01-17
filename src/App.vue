<template>
  <div id="app">
    <h1>Countries Of The World</h1>
    <div class="">
      <country-form :countries="countries"></country-form>
    </div>
  </div>
</template>

<script>
import CountryForm from './components/countryForm.vue'

export default {
  name: 'app',
  components: {
    "country-form": CountryForm
  },
  data() {
    return {
      countries: []
    }
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
      .then(response => response.json())
      .then(objectsArray => this.countries = objectsArray)
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
