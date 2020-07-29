<template>
  <fieldset v-if="country" :style="flagStyle">
    <legend>{{country.name}}</legend>
    <div class="details">
      <ul>
        <li>
          <span class="key">Population:</span>
          <span class="value">{{country.population | numberFormatter}}</span>
        </li>
        <li>
          <span class="key">Capital:</span>
          <span class="value">{{country.capital}}</span>
        </li>
        <li>
          <span class="key">Languages:</span>
          <span
            class="value lang"
            v-for="(lang, index) in country.languages"
            :key="index"
          >{{lang.name}}</span>
        </li>
      </ul>
    </div>
    <div class="flag">
      <img class="flag-lg" :src="country.flag" />
    </div>
  </fieldset>
</template>

<script>
export default {
  name: "country-detail",
  props: ["country"],
  filters: {
    numberFormatter(num) {
      return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,");
    },
  },
};
</script>

<style scoped>
fieldset {
  border: 3px groove;
  width: 600px;
  height: 300px;
  background-color: #716a5c;
  padding: 2em;
}
legend {
  font-size: 24px;
}
.details {
  float: left;
}
.flag {
  border: 3px groove;
  float: right;
  width: 15em;
  height: 9em;
}
.flag-lg {
  height: 100%;
  width: 100%;
}
.key {
  width: 8em;
}
.lang::after {
  content: ", \00a0";
}
.lang:last-child::after {
  content: "";
}
</style>