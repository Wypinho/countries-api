<template lang="html">
  <div class="">
    <h3 v-if="countries.length">Favourite Countries</h3>
    <ul>
      <li v-for="country in countries">{{country.name}} <img class="flag-small" :src="country.flag"></li>
    </ul>
  </div>

</template>

<h4 v-if="neighbours.length">Neighbours:</h4>
<p>Combined Population of Neighbours: {{neighboursPopulation}}</p>
<ul>
  <li v-for="neighbour in neighbours">{{neighbour.name}} <img class="flag-small" :src="neighbour.flag"></li>
</ul>

<script>
export default {
  name: 'favourite-countries',
  props: ['countries']
}
</script>

<style lang="css" scoped>
</style>
