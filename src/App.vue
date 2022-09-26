<template>
  <BitcoinData />
</template>

<script>
import BitcoinData from './components/BitcoinData.vue';

export default {
  name: 'App',
  components: {
    BitcoinData
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
