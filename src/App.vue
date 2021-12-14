<template>
  <div id="app">
    <div class="jumbotron">
      <CurrencyConverter />
    </div>
  </div>
</template>

<script>
import CurrencyConverter from "./components/CurrencyConverter.vue";

export default {
  name: "App",
  components: {
    CurrencyConverter,
  },
};
</script>
