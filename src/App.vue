<template>
  <div id="app">
    <TheNavBar :genres-list="genresList" @onGenreSelect="onGenreSelect" :artists-list="artistsList" @onArtistSelect="onArtistSelect" />
    <AlbumsList :selected-genre="selectedGenre" @onGenresListCreation="onGenresListCreation" :selected-artist="selectedArtist" @onArtistsListCreation="onArtistsListCreation"/>
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
        selectedGenre: "",
        artistsList: [],
        selectedArtist: ""
      }
    },

    methods: {
      onGenresListCreation(genresList) {
        this.genresList = genresList;
      },
      onGenreSelect(genre) {
        this.selectedGenre = genre;
      },
      onArtistsListCreation(artistsList) {
        this.artistsList = artistsList;
      },
      onArtistSelect(artist) {
        this.selectedArtist = artist;
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
