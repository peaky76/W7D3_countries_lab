<template>
  <input v-on:input="handleInput" type="text" v-model="searchTerm" />
</template>

<script>
import { eventBus } from "../main.js";

export default {
  data() {
    return {
      searchTerm: null,
    };
  },
  methods: {
    handleInput() {
      eventBus.$emit("search-term", this.searchTerm);
    },
  },
};
</script>

<style>
</style>