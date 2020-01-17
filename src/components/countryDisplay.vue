<template lang="html">
  <article v-if="country">
    <h3>{{country.name}}</h3>
    <img :src="country.flag" alt="">
  </article>
</template>

<script>
export default {
  name: 'country-display',
  props: ['country']
}
</script>

<style lang="css" scoped>
</style>
