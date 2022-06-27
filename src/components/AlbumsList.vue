<template>
    <main class="flex-grow-1">
        <div class="container h-100">
            <div class="row h-100 align-items-center">
                <AlbumsLoader v-if="loadingAlbums"/>
                <div class="row row-cols-5 gx-5 gy-3">
                    <AlbumCard v-for="album in filteredAlbums" :key="album.title" :album="album"/>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
    import AlbumsLoader from './AlbumsLoader.vue';
    import AlbumCard from './AlbumCard';
    import axios from "axios";

    export default {
        components: {
            AlbumsLoader,
            AlbumCard
        },

        props: {
            selectedGenre: String,
            selectedArtist: String
        },

        data() {
            return {
                albumsList: [],
                loadingAlbums: false
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
            getArtistsList() {
                const artistsList = [];
                this.albumsList.forEach((album) =>{
                    if(!artistsList.includes(album.author)) {
                        artistsList.push(album.author);
                    }
                });
                return artistsList;
            },
            filteredAlbums() {
                if(!this.selectedGenre && !this.selectedArtist) {
                    return this.albumsList;
                } else if (!this.selectedGenre) {
                    return this.albumsList.filter((album) =>{
                        return album.author === this.selectedArtist;
                    });
                } else if (!this.selectedArtist) {
                    return this.albumsList.filter((album) =>{
                        return album.genre === this.selectedGenre;
                    });
                }
                return this.albumsList.filter((album) =>{
                    return album.genre === this.selectedGenre && album.author === this.selectedArtist;
                });
            }
        },

        methods: {
            fetchAlbumsList() {
                this.loadingAlbums = true;
                axios.get("https://flynn.boolean.careers/exercises/api/array/music").then((response) => {
                    this.albumsList = response.data.response;
                    this.$emit("onGenresListCreation", this.getGenresList);
                    this.$emit("onArtistsListCreation", this.getArtistsList);
                    setTimeout(() => {
                        this.loadingAlbums = false;
                    }, 1000);
                });
            }
        },

        mounted() {
            this.fetchAlbumsList();
        }
    }
</script>