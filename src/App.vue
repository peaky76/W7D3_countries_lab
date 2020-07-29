<template>
  <div>
    <h1>Countries of the world</h1>
    <div class="main-container">
      <countries-list :countries="countries"></countries-list>
      <country-detail :country="selectedCountry"></country-detail>
    </div>
  </div>
</template>

<script>
import CountryDetail from "./components/CountryDetail.vue";
import CountriesList from "./components/CountriesList.vue";
import { eventBus } from "./main.js";

export default {
  data() {
    return {
      countries: [],
      selectedCountry: null,
    };
  },
  mounted() {
    fetch("https://restcountries.eu/rest/v2/all")
      .then((response) => response.json())
      .then((data) => (this.countries = data));

    eventBus.$on("selected-country", (country) => {
      this.selectedCountry = country;
    });
  },
  components: {
    "country-detail": CountryDetail,
    "countries-list": CountriesList,
  },
};
</script>

<style>
</style>
