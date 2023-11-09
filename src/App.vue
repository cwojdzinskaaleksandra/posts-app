<template>
  <main>
    <drop-down :options="options" v-model="parentSelectedOption" />
    <br />
    <h1>Selected option: {{ parentSelectedOption }}</h1>
  </main>
</template>

<script setup>
import { ref } from "vue";
import DropDown from "./components/DropDown.vue";

const options = ref([
  {
    name: "One",
    value: 1,
  },
  {
    name: "Two",
    value: 2,
  },
  {
    name: "Three",
    value: 3,
  },
  {
    name: "Four",
    value: 4,
  },
]);

const parentSelectedOption = ref(null);
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
main {
  max-width: 500px;
  margin: 0 auto;
}
</style>
