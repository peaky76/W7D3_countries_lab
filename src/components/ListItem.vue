<template>
  <li v-on:click="handleClick">
    <img class="flag-sm" :src="country.flag" />
    <div class="country-name">{{country.name}}</div>
  </li>
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
li {
  display: flex;
  align-items: flex-start;
  margin-bottom: 0.5em;
}

.country-name {
  border-top: 0.125em groove #ff9000;
  padding: 0.25em;
}
.country-name:hover {
  background-color: #ff9000;
  cursor: pointer;
}
</style>