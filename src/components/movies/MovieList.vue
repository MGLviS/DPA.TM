<template>
        <div class="dropdown">
        <label for="numberDropdown">Numero Página: </label>
        <select 
            id="numberDropdown" 
            v-model="selectedNumber" 
            @change="handleNumberChange">
          <option v-for="number in numbers" :key="number" :value="number">{{ number }}</option>
        </select>
      </div>
    <div class="titulo-lista"><h6> Peliculas disponibles</h6></div>

    <div class="movie-list">
        <div class="movie-grid">
            <div class="movie-item" v-for="movie in movies" :key="movie.id">
                <MovieItem :movie="movie" />
            </div>
        </div>
    </div>
</template>

<style>
.dropdown {
    display: flex;
    justify-content: right;
    margin-left: 3%;
    
}
.titulo-lista {
    margin-left: 2%;
}
.movie-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 60px;
}
.movie-item {
    margin-left: 5%;
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

            var page = this.selectedNumber
            var url = "https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page="+page+"&sort_by=popularity.desc"
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

        },
        handleNumberChange() {
            // Este método se ejecutará cuando cambie la opción seleccionada en la lista desplegable
            console.log("Número cambiado:", this.selectedNumber);
            this.getMovie();
        },
    },

    data() {
        return {
            movies: [],
            selectedNumber: 1,
            numbers: Array.from({ length: 20 }, (_, index) => index + 1),
        }
    },
    
}

</script>