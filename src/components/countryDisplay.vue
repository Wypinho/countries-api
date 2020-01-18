<template lang="html">
  <article v-if="country">
    <div class="">
      <h3>{{country.name}}</h3>
      <button type="button" name="button">Add to Favourites</button>
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

.flag-large {
  height: 300px;
  /* width: 500px; */
  display: block;
  margin-left: auto;
  border: solid 1px;
}

.flag-small {
  height: 30px;
  border: solid 1px;
}

dt, dd {
  display: inline-grid;
}

</style>
