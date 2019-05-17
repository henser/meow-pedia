<template>
  <div id="app">
    <Kittens msg="meow!"/>
  </div>
</template>

<script>
import Kittens from './components/Kittens.vue'

export default {
  name: 'app',
  components: {
    Kittens
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
