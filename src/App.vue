<template>
  <div id="app">
    <Header/>
    <Kittens />
  </div>
</template>

<script>
import Header from './components/Header'
import Kittens from './components/Kittens'

export default {
  name: 'app',
  components: {
    Header,
    Kittens
  }
}
</script>

<style>

html,
body {
  background-color: #fafafa;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
