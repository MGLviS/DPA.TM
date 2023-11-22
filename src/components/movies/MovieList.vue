<template>
    <h6> Lista Peliculas</h6>
    <div class="movie-list">
        <div class="movie-grid">
            <div class="movie-item" v-for="movie in movies" :key="movie.id">
                <MovieItem :movie="movie" />
            </div>
        </div>
    </div>
</template>

<style>
.movie-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 60px;
}
</style>

<script>
import MovieItem from 'components/movies/MovieItem.vue'
import axios from 'axios'


export default {
    name: "MovieList",
    components: {
        MovieItem
    },

    mounted() {
        this.getMovie()
    },

    methods: {
        getMovie() {

            var url = "https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc"
            var token = "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI4YWJlMTE3NWVjNzVkNDY3NDMxNjM4ZjRkYjhhZDFhYiIsInN1YiI6IjY1NWEyODY1NTM4NjZlMDBmZjA5NTkwMSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.uSfAXqK_k6B-LtXJjSFXego87_udgBySiAZV7HdcMno"
            var header = {
                headers: {
                    Authorization: 'Bearer ' + token
                }
            }
            axios.get(url,header)
                .then(response => {
                    this.movies = response.data.results
                }).catch(error => {
                    console.log("Error: " + error)
                })

        }
    },

    data() {
        return {
            movies: []
        }
    }
    
    
}

</script>