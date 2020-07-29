<template>
  <li v-on:click="handleClick">This is a country {{country.name}}</li>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "list-item",
  props: ["country"],
  methods: {
    handleClick() {
      eventBus.$emit("selected-country", this.country);
    },
  },
};
</script>

<style>
</style>