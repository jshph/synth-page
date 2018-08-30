<template>
  <div id="app">
    <SynthApp/>
  </div>
</template>

<script>
import SynthApp from './components/SynthApp.vue'

export default {
  name: 'app',
  components: {
    SynthApp
  }
}
</script>

<style>
.app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
