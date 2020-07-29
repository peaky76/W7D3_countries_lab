<template>
  <div class="main-container">
    <h1>Countries of the world</h1>
    <search-form></search-form>
    <br />
    <br />
    <!-- <countries-dropdown :countries="countries"></countries-dropdown> -->
    <country-detail :country="foundCountry"></country-detail>
  </div>
</template>

<script>
// import CountriesDropdown from "./components/CountriesDropdown.vue";
import { eventBus } from "./main.js";
import CountryDetail from "./components/CountryDetail.vue";
import SearchForm from "./components/SearchForm.vue";

export default {
  data() {
    return {
      countries: [],
      searchTerm: null,
    };
  },
  computed: {
    countryLookUp() {
      const matchCountries = this.countries.filter((country) => {
        const length = this.searchTerm.length;
        if (length === 0) {
          return true;
        }
        if (
          country.name.toLowerCase().substring(0, length) ===
          this.searchTerm.toLowerCase()
        ) {
          return true;
        }
        return false;
      });
      return matchCountries;
    },
    foundCountry() {
      if (this.countryLookUp.length === 1) {
        return this.countryLookUp[0];
      } else {
        return null;
      }
    },
  },
  mounted() {
    fetch("https://restcountries.eu/rest/v2/all")
      .then((response) => response.json())
      .then((data) => (this.countries = data));

    // eventBus.$on("selected-country", (country) => {
    //   this.selectedCountry = country;
    // });

    eventBus.$on("search-term", (term) => {
      this.searchTerm = term;
    });
  },
  components: {
    "search-form": SearchForm,
    "country-detail": CountryDetail,
    // "countries-dropdown": CountriesDropdown,
  },
};
</script>

<style>
body,
select {
  background: #5f021f;
  color: #f4fffd;
  font-family: "Crete Round", serif;
}
/* Destyle */
ul {
  list-style: none;
  padding: 0;
}

select {
  font-size: 1em;
}

select:focus {
  outline: none;
}

.flag-sm {
  width: 3em;
}
</style>
