<template>
  <div id="app">
    <!-- Header -->
    <header class="p-3">
      <img class="h-100" src="./assets/img/logo-small.svg" alt="">
    </header>
    <!-- Main content -->
    <main>
      <div class="container h-100">
        <div class="row h-100 align-items-center">
          <div class="row row-cols-5 gx-5 gy-3">
            <AlbumCard v-for="album in albumsList" :key="album.title" 
            :album-cover-url="album.poster" 
            :album-title="album.title" 
            :album-author="album.author" 
            :album-release-year="album.year"/>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import AlbumCard from './components/AlbumCard.vue'
import axios from "axios";

export default {
  name: 'App',
  components: {
    AlbumCard
  },
  data() {
    return {
      albumsList: []
    }
  },
  methods: {
    fetchAlbumsList() {
      axios.get("https://flynn.boolean.careers/exercises/api/array/music")
        .then((response) => {
          this.albumsList = response.data.response;
        });
    }
  },
  mounted() {
    this.fetchAlbumsList();
  }
}
</script>

<style lang="scss">
#app {
  height: 100vh;
  background-color: #1E2D3B;

  header {
    height: 7vh;
    background-color: #2E3A46;
  }
  main {
    height: 93vh;
  }
}
</style>
