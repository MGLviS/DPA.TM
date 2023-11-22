<template>
    <div class="movie-title">
        TMDB
    </div>
    <div class="movie-page">
        
        <div class="movie-list">
            <MovieList />
        </div>
    </div>

</template>

<style>
.movie-title {
    text-align: center;
    font-size: 150%;
    margin-top: 2%;
}
.movie-page {
    display: flex;
    justify-content: space-between;
}

.movie-list {
    width: 99%;
}
</style>

<script>

import MovieList from 'src/components/movies/MovieList.vue'
export default {
    name: "MoviePage",
    components: {
        MovieList
    }
}
</script>