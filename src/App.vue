<template>
  <div id="app">
    <conversor currencyA="EUR" currencyB="BRL"/>
  </div>
</template>

<script>
import Conversor from"./components/Conversor.vue";
export default {
  name: 'App',
  components: {
    Conversor
  }
};
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  z-index: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

 
}
</style>

