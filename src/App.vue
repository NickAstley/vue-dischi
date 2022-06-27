<template>
  <div id="app">
    <TheNavBar :genres-list="getGenresList" @onGenreSelect="onGenreSelect"/>
    <main class="flex-grow-1">
      <div class="container h-100">
        <div class="row h-100 align-items-center">
          <div class="row row-cols-5 gx-5 gy-3">
            <AlbumCard v-for="album in filteredAlbums" :key="album.title" :album="album"/>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
  import TheNavBar from './components/TheNavBar';
  import AlbumCard from './components/AlbumCard';
  import axios from "axios";

  export default {
    name: 'App',
    components: {
      TheNavBar,
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
        if(!this.selectedGenre) {
          return this.albumsList;
        }
        return this.albumsList.filter((album) =>{
          return album.genre === this.selectedGenre;
        });
      }
    },

    methods: {
      fetchAlbumsList() {
        axios.get("https://flynn.boolean.careers/exercises/api/array/music")
          .then((response) => {
            this.albumsList = response.data.response;
          });
      },
      onGenreSelect(genre) {
        this.selectedGenre = genre;
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
    display: flex;
    flex-direction: column;
    background-color: #1E2D3B;
  }
</style>
