<template>
    <div>
        <div class="album-card p-4 text-center h-100">
            <img class="w-100 mb-3" :src="albumPoster" :alt="album.title" @error="onImageLoadError">
            <h4 class="text-white text-uppercase mb-3">{{ album.title }}</h4>
            <div class="album-author">{{ album.author }}</div>
            <span>{{ album.year }}</span>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            album: Object
        },

        data() {
            return {
                albumPoster: ""
            }
        },

        methods: {
            onImageLoadError() {
                this.albumPoster = "https://upload.wikimedia.org/wikipedia/en/2/2c/Bon_Jovi_New_Jersey.jpg";
            }
        },

        mounted() {
            this.albumPoster = this.album.poster;
        }
    }
</script>

<style lang="scss">
    .album-card {
        background-color: #2E3A46;
        color: #6E6D6E;

        .album-author {
            font-size: 1.2rem;
        }
    }
</style>