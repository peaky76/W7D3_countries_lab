<template>
  <div v-if="country">
    <ul>
      <li>{{country.name}}</li>
      <li>{{country.capital}}</li>
      <li>{{country.population}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "country-detail",
  props: ["country"],
};
</script>

<style>
</style>