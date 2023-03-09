<template>
  <numberToRomain msg="Number to roman letters conversion"/>
</template>

<script>
import numberToRomain from './components/numberToRomain.vue'

export default {
  name: 'App',
  components: {
    numberToRomain
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
