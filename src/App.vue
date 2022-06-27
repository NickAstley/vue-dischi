<template>
  <div id="app">
    <TheNavBar :genres-list="genresList" @onGenreSelect="onGenreSelect"/>
    <AlbumsList :selected-genre="selectedGenre" @onGenresListCreation="onGenresListCreation"/>
  </div>
</template>

<script>
  import TheNavBar from './components/TheNavBar';
  import AlbumsList from './components/AlbumsList';

  export default {
    name: 'App',
    
    components: {
      TheNavBar,
      AlbumsList
    },
    
    data() {
      return {
        genresList: [],
        selectedGenre: ""
      }
    },

    methods: {
      onGenresListCreation(genresList) {
        this.genresList = genresList;
      },
      onGenreSelect(genre) {
        this.selectedGenre = genre;
      }
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
