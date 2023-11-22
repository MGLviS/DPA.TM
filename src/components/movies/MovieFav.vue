<template>
    <div>
      <q-dialog v-model="mostrarModal">
        <q-card class="qcard-modal-edit">
          <q-card-section>
            <div class="titulo">Favoritos </div>

            <div class="movie-item" v-for="movie in movieFav" :key="movie.id">
            
            <q-card-section>
            
            <q-img 
                :src="'https://image.tmdb.org/t/p/w500/'+movie.poster_path"
            >
            </q-img>
        </q-card-section>
        <q-card-section>      
            <div class="text-h6 font-weight-bold">{{ movie.title }}</div>
            <q-icon name="stars" size="1.8em" color="warning"/>
            {{movie.vote_average}}/10
            <div class="text-subtitle2">
                <br/>
                
            </div>
      
            <q-expansion-item
                expand-separator
                icon="description"
                label="Sinopsis"
            >
                <q-card>
                <q-card-section>
                {{ movie.overview }}
                </q-card-section>
                </q-card>
                </q-expansion-item>
        
        </q-card-section>
        </div>
            <div class="buttons">
              <q-btn @click="cerrarModal" label="Cerrar" color="red" />
            </div>
          </q-card-section>
        
        </q-card>
      </q-dialog>
    </div>
  </template>

  <style>
  .titulo{
    text-align: center;
    font-size: large;
    font-style: inherit;
  }
  .qcard-modal-edit {
    width: 550px;
    align-content: center;
  }

  .buttons {
    display: flex;
    justify-content: space-between;
    margin-top: 25px;
  }

  .buttons q-btn {
    width: 48%;

  }

  .buttons q-btn:last-child {
    margin-left: 10px;
  }

  .custom-label .q-field__label {
  font-size: 16px;

}
  </style>





<script>
import axios from 'axios'
export default {

    

    data(){
        return {
            mostrarModal: false,
            movieFav: []
        }
    },

    methods: {
        abrirModalnuevoV() {
            this.mostrarModal = true;
            this.getMovieFav();
        },

            // Método para cerrar el modal de edición
        cerrarModal() {
            this.mostrarModal = false;
            // Limpia los campos de edición
        },

        getMovieFav() {

            var url = "https://api.themoviedb.org/3/account/20722641/favorite/movies?language=en-US&page=1&sort_by=created_at.asc"
            var token = "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI4YWJlMTE3NWVjNzVkNDY3NDMxNjM4ZjRkYjhhZDFhYiIsInN1YiI6IjY1NWEyODY1NTM4NjZlMDBmZjA5NTkwMSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.uSfAXqK_k6B-LtXJjSFXego87_udgBySiAZV7HdcMno"
            var header = {
                headers: {
                    Authorization: 'Bearer ' + token
                }
            }
            axios.get(url,header)
                .then(response => {
                    this.movieFav = response.data.results
                    console.log(this.movieFav)
                }).catch(error => {
                    console.log("Error: " + error)
                })

        }
    }
}
</script>