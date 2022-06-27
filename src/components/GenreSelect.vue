<template>
    <form class="float-end">
        <label class="visually-hidden" for="genreSelect">Genre</label>
        <select class="form-select" id="genreSelect" v-model="selectedGenre" @change="onGenreSelect()">
            <option selected value="">Seleziona un genere..</option>
            <option v-for="genre in genresList" :key="genre" :value="genre">{{ genre }}</option>
        </select>
    </form>
</template>

<script>
    export default {
        props: {
            genresList: Array
        },

        data() {
            return {
                selectedGenre: ""
            }
        },
        
        methods: {
            onGenreSelect() {
                this.$emit("onGenreSelect", this.selectedGenre);
            }
        }
    }
</script>