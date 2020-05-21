<template>
  <div id="app">
    <FighTheMonster msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import FighTheMonster from './components/FighTheMonster.vue'

export default {
  name: 'App',
  components: {
    FighTheMonster
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
}
</style>
