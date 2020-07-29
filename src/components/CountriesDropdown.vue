<template>
  <select v-on:change="handleChange" v-model="selectedCountry">
    <option
      v-for="(country, index) in countries"
      :value="country"
      :country="country"
      :key="index"
    >{{country.name}}</option>
  </select>
</template>

<script>
import { eventBus } from "../main.js";
export default {
  name: "countries-dropdown",
  data() {
    return {
      selectedCountry: null,
    };
  },
  props: ["countries"],
  methods: {
    handleChange() {
      eventBus.$emit("selected-country", this.selectedCountry);
    },
  },
};
</script>

<style>
</style>