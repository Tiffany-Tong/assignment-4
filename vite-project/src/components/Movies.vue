<script setup>
import { ref } from "vue";
import axios from "axios";
 
const response = ref("");
const movie = ref(null);
 
const getMovies = async () => {
  const data = response.value;
  movie.value = (
    await axios.get(`https://api.themoviedb.org/3/movie/${data}`, {
      params: {
        api_key: "c6b2390c3ab4bfbd0e064d952df483c9",
        append_to_response: "videos",
      },
    })
  ).data;
};
</script>
 
<template>
<h1 class="title"> Choose a movie from the dropdown <br> menu and press Get for movies: </h1>

  <select v-model="response">
    <option value="">Choose a Movie:</option>
        <option value="93456">Despicable Me 2</option>
        <option value="527641">Five Feet Apart</option>
        <option value="177572">Big Hero 6</option>
        <option value="623195">Falling Inn Love</option>
        <option value="37056">Letters to Juliet</option>
        <option value="713776">If Anything Happens I Love You</option>
        <option value="207">Dead Poets Society</option>
        <option value="772272">Tall Girl 2</option>
        <option value="934761">A Perfect Pairing</option>
        <option value="585">Monster Inc</option> 
  </select>
  <button @click="getMovies">Get</button>
  <div v-if="movie" class="movie-container">
    <p>{{movie.original_title}}</p>
    <p>{{movie.overview}}</p>
    <p>{{movie.release_date}}</p>
    <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`">
    <iframe :src="`https://www.youtube.com/embed/${movie.videos.results.filter((video) => video.type === 'Trailer').at(0).key}`"></iframe>
  </div>
</template>
 
<style scoped>
h1{
  text-align: center;
  font-size: 65px;
  color: black;
  font-family: 'Times New Roman', Times, serif;
}

p{
  color: black;
  text-align: center;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
 
img{
  width: 200px;
  aspect-ratio: 2 / 3;
}
 
iframe{
  aspect-ratio: 16 / 9;
  height: 300px;
}

select{
  color: black;
  text-align: center;
}
 
button{
  color: black;
  text-align: center;
}
</style>