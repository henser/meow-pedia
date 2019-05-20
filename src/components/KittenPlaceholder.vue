<template>
  <b-card class="w-100 p-4 mb-4 border-0 shadow-sm mx-4 mx-sm-auto">
    <span class="card-ph card-ph-img"></span>
    <b-card-body class="d-flex flex-column p-0">
      <span class="card-ph"></span>
    </b-card-body>
    <b-card-footer class="bg-white border-0">
      <span class="card-ph"></span>
    </b-card-footer>
  </b-card>
</template>

<script>
export default {
  name: 'KittenPlaceholder'
}
</script>

<style scoped>

.card-ph {
  display: block;
  width: 100%;
  border-radius: none;
  animation: pulse 1s infinite ease-in-out;
  height: 20px;
  margin-bottom: 20px;
}

.card-ph-img {
  height: 140px;
}

@keyframes pulse {
    0% {
        background-color: rgba(165, 165, 165, 0.1);
    }
    50% {
        background-color: rgba(165, 165, 165, 0.3);
    }
    100% {
        background-color: rgba(165, 165, 165, 0.1);
    }
}
</style>
