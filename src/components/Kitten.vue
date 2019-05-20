<template>
  <b-card class="w-100 mb-4 border-0 shadow-sm mx-4 mx-sm-auto">
    <b-card-header class="d-flex justify-content-center align-items-center bg-white p-0 border-0">
      <b-card-img-lazy class="w-auto mw-100" :src="item.url" :alt="item.breeds[0].alt_names" blank-src="load-img.svg"></b-card-img-lazy>
    </b-card-header>
    <b-card-body class="d-flex flex-column pb-0">
      <b-card-title> {{ item.breeds[0].name }} </b-card-title>
      <b-card-text class="d-flex flex-column justify-content-between h-100">
          {{ item.breeds[0].origin }}
      </b-card-text>
    </b-card-body>
    <b-card-footer class="bg-white border-0 pb-0">
      <b-link :href="item.breeds[0].wikipedia_url" target='_blank'> Read more </b-link>
    </b-card-footer>
  </b-card>
</template>

<script>
export default {
  name: 'Kitten',
  props: {
    item: Object
  }
}
</script>

<style scoped>

.kittens .card-header {
  height: 180px;
}

.kittens .card-body .card-img {
  max-height: 180px;
}

</style>
