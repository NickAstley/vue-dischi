<template>
<div>
    <div class="album-card p-4 text-center h-100">
        <img class="w-100 mb-3" :src="album.poster" :alt="album.title">
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