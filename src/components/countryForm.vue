<template lang="html">
  <select class="" name="">
    <option v-for="country in countries">{{country.name}}</option>
  </select>
</template>

<script>
export default {
  name: 'country-form',
  props: ['countries']
}
</script>

<style lang="css" scoped>
</style>
