<template>
    <header class="p-3">
        <nav>
            <img class="spotify-logo" src="../assets/img/logo-small.svg" alt="Logo Spotify">
            <GenreSelect :genres-list="genresList" @onGenreSelect="$emit('onGenreSelect', $event)"/>        
            <ArtistSelect :artists-list="artistsList" @onArtistSelect="$emit('onArtistSelect', $event)"/>        
        </nav>
    </header>
</template>

<script>
    import GenreSelect from './GenreSelect';
    import ArtistSelect from './ArtistSelect';

    export default {
        components: {
            GenreSelect,
            ArtistSelect
        },

        props: {
            genresList: Array,
            artistsList: Array
        }
    }
</script>

<style lang="scss" scoped>
  header {
    background-color: #2E3A46;
    
    .spotify-logo {
      width: 50px;
    }
  }
</style>