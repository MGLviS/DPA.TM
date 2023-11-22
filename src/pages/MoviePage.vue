<template>
    <div class="movie-title">
        TMDB
    </div>
    <div class="btn-fav">
            <MovieFav ref="MovieFav" />
            <div class="agregar">
                <q-btn 
                    @click="movief" 
                    color="red" 
                    icon="favorite" 
                    label="Mis Favoritos" />
                <br/>
            </div>
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

.btn-fav {
    text-align: left;
    margin-left: 2%;
}
</style>

<script>

import MovieList from 'src/components/movies/MovieList.vue'
import MovieFav from 'src/components/movies/MovieFav.vue'
export default {
    name: "MoviePage",
    components: {
        MovieList,
        MovieFav
    },

    methods: {
        movief(){
            this.$refs.MovieFav.abrirModalnuevoV();
        }
    }
}
</script>