<template>
  <div id="app">
    <!-- Header -->
    <header class="p-3">
      <img class="h-100" src="./assets/img/logo-small.svg" alt="Logo Spotify">
      <form class="float-end">
        <div>
          <label class="visually-hidden" for="genreSelect">Genre</label>
          <select class="form-select" id="genreSelect" v-model="selectedGenre">
            <option selected value="">Seleziona un genere..</option>
            <option v-for="genre in getGenresList" :key="genre" :value="genre">{{ genre }}</option>
          </select>
        </div>
      </form>
    </header>
    <!-- Main content -->
    <main>
      <div class="container h-100">
        <div class="row h-100 align-items-center">
          <div class="row row-cols-5 gx-5 gy-3">
            <AlbumCard v-for="album in filteredAlbums" :key="album.title" 
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
      albumsList: [],
      selectedGenre: ""
    }
  },
  computed: {
    getGenresList() {
      const genresList = [];
      this.albumsList.forEach((album) =>{
        if(!genresList.includes(album.genre)) {
          genresList.push(album.genre);
        }
      });
      return genresList;
    },
    filteredAlbums() {
      const filteredAlbums = [];
      this.albumsList.forEach((album) =>{
      if(album.genre.includes(this.selectedGenre)) {
        filteredAlbums.push(album);
      }
      });
      return filteredAlbums;
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
