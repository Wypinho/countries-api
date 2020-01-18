<template lang="html">
  <article v-if="country">
    <div class="">
      <h3>{{country.name}}</h3>
      <button v-on:click="handleClick">Add to Favourites</button>
      <dl>
        <dt>Capital:</dt>
        <dd>{{country.capital}}</dd>
        <br>
        <dt>Population:</dt>
        <dd>{{country.population}}</dd>
        <br>
        <dt>Region:</dt>
        <dd>{{country.region}}</dd>
      </dl>
      <h4 v-if="neighbours.length">Neighbours:</h4>
      <p>Combined Population of Neighbours: {{neighboursPopulation}}</p>
      <ul>
        <li v-for="neighbour in neighbours">{{neighbour.name}} <img class="flag-small" :src="neighbour.flag"></li>
      </ul>
    </div>
    <div class="">
      <img class="flag-large":src="country.flag" alt="">

    </div>


  </article>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'country-display',
  props: ['country', 'countries'],
  computed: {
    neighbours: function() {
      return this.countries.filter((country) => {
        return this.country.borders.includes(country.alpha3Code)
      })
    },
    neighboursPopulation: function() {
      return this.populationCalculator(this.neighbours)
    }
  },
  methods: {
    populationCalculator: function(countries){
        return countries.reduce((runningTotal, country) => runningTotal + country.population, 0);
      },
    handleClick(){
        eventBus.$emit('favourite', this.country.alpha3Code)
    }
  }
}
</script>

<style lang="css" scoped>

article {
  display: grid;
  grid-template-columns: auto auto;
}

h3  {
  text-align: left;
}



dt, dd {
  display: inline-grid;
}

</style>
