<template>
  <Conversor />
</template>

<script>
import Conversor from"./components/Conversor";

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
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; 
}
</style>

