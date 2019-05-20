<template>
  <div class="kittens">
    <section class="section">
      <!-- Start: Card -->
      <div class="container">
        <div class="row">
          <div v-for="(item, $index) in results" :key="$index" class="col-md-6 col-lg-4 d-flex h-auto">
            <kitten :item="item"></kitten>
          </div>
        </div>
        <div class="row" v-show="this.processing">
          <div v-for="(item, $index) in limit" :key="$index" class="col-md-6 col-lg-4 d-flex h-auto">
            <kitten-placeholder></kitten-placeholder>
          </div>
        </div>
      </div>
      <!-- End: Card -->
    </section>
    <!-- Start: Infinite Loading-->
    <infinite-loading :distance="distance" :identifier="infiniteId" @infinite="infiniteHandler">
      <div slot="spinner">
        <img class="kittens-spinner my-4" src="logo.svg" alt="Meow-Pedia! logo" />
      </div>
      <div slot="no-more">
        <img class="my-4" src="loaded.svg" alt="Meow-Pedia! all done" />
      </div>
      <div slot="no-results">Kittens are hidden!</div>
    </infinite-loading>
    <!-- End: Infinite Loading-->
  </div>
</template>

<script>

import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import InfiniteLoading from 'vue-infinite-loading'

import Kitten from './Kitten'
import KittenPlaceholder from './KittenPlaceholder'

Vue.use(VueAxios, axios)

const apiParams = {}

export default {
  name: 'Kittens',
  components: {
    InfiniteLoading,
    Kitten,
    KittenPlaceholder
  },
  data () {
    return {
      page: 0,
      limit: 6,
      loaded: 0,
      loadedIndex: 0,
      results: [],
      processing: false,
      distance: parseInt(window.innerHeight * 2),
      infiniteId: +new Date()
    }
  },
  methods: {
    infiniteHandler ($state) {
      apiParams.page = this.page;
      apiParams.limit = this.limit;

      if (this.processing) {
        return;
      }

      this.processing = true;

      axios.get(process.env.VUE_APP_CAT_API_PATH + '/breeds', {
        params: apiParams
      }).then(response => {
        let data = response.data;

        if (data.length) {
          this.getImages(data, $state).then(() => {
            this.page++;
            this.infiniteId++;
            this.loadedIndex = 0;
            $state.loaded();
            this.processing = false;
          });

        } else {
          $state.loaded();
          $state.complete();
          this.processing = false;
        }

      });

    },
    async getImages (data, $state) {
      let breed = data[this.loadedIndex];

      let img = await axios.get(process.env.VUE_APP_CAT_API_PATH + '/images/search', {
        params: { breed_ids: breed.id, limit: 1 }
      });

      return this.getImage(img, data, $state);
    },
    getImage (r, data, $state) {
      this.results[this.loaded] = r.data[0];
      this.loaded++;
      this.loadedIndex++;

      return this.loaded % this.limit === 0 || data.length < this.limit ? '' : this.getImages(data, $state);
    }

  }
}
</script>

<style scoped>

.kittens {
  background-color: #fafafa;
  padding-top: 30px;
}

.kittens-spinner {
  animation: rotation 2s infinite linear;
}

@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(359deg);
  }
}

a {
  color: #42b983;
}
</style>
