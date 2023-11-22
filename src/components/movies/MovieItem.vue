<template>
    <q-card class="movie-card">
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
            <q-checkbox 
                fab
                v-model="favorite" 
                checked-icon="favorite"
                unchecked-icon="favorite_border"
                color="red"
                size="4em"
                class="absolute"
                style="top: 32px; right: 12px; transform: translateY(-50%);"
            />
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
    </q-card>
</template>


<style>
.movie-card {
    width: 300px;
}

.movie-card q-card-section {
    height: 100px;
    overflow: hidden;
    
}
</style>


<script>
import { ref } from 'vue'

export default {
    name: "MovieItem",
    props: {
        movie: {
            type: Object,
            required: true
        }
    },
    setup () {
        return {
        favorite: ref(false)
        }
    }
}
</script>