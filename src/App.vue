<template>
  <div>
    <CalculatorApp />
  </div>
</template>

<script>
import CalculatorApp from "./components/CalculatorApp.vue";

export default {
  name: "App",
  components: {
    CalculatorApp,
  },
};
</script>

<style>
html {
  height: 100vh;
  background: linear-gradient(to bottom right, #264653, #2a9d90);
  background-repeat: no-repeat;
}
</style>
