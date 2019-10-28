<template>
  <div id="app">
    <Calculator msg="Hello, I am a calculator" />
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "app",
  components: {
    Calculator
  }
};
</script>

<style>
body {
  background: #c6cbef;
}
</style>
