<template lang="html">
  <article v-if="country">
    <div class="">
      <h3>{{country.name}}</h3>
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
    </div>
    <div class="">
      <img class="flag-large":src="country.flag" alt="">

    </div>


  </article>
</template>

<script>
export default {
  name: 'country-display',
  props: ['country']
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
  display: block;
  margin-left: auto;
}

dt, dd {
  display: inline-grid;
}

</style>
