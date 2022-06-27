<template>
    <form class="float-end">
        <label class="visually-hidden" for="artistSelect">Artist</label>
        <select class="form-select" id="artistSelect" v-model="selectedArtist" @change="onArtistSelect()">
            <option selected value="">Seleziona un artista..</option>
            <option v-for="artist in artistsList" :key="artist" :value="artist">{{ artist }}</option>
        </select>
    </form>
</template>

<script>
    export default {
        props: {
            artistsList: Array
        },

        data() {
            return {
                selectedArtist: ""
            }
        },
        
        methods: {
            onArtistSelect() {
                this.$emit("onArtistSelect", this.selectedArtist);
            }
        }
    }
</script>