<template>
  <header class="header bg-dark shadow-sm">
    <div class="container d-flex align-items-center h-100">
        <img class="logo" src="logo.svg" alt="Meow-pedia! logo">
        <span class="title pl-2"> {{ title }} </span>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      title: process.env.VUE_APP_TITLE
    }
  }
}
</script>

<style scoped>
.header {
  height: 70px;
  color: #fff;
}

.header .title {
  font-size: 22px;
  font-weight: bold;
}

a {
  color: #42b983;
}
</style>
