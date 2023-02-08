<template>
  <div id="app">
    <div class="container">
      <div class="text-center">
        <h2 class="text-center mt-5">Trending Movies 🍿</h2>
        <p>Keep up with the hottest movies that are trending this week.</p>
      </div>

      <div class="my-4">
        <a href="#" @click="getTrendingMovies('day')" class="mx-3 h4">
          Trending today</a
        >
        <a href="#" @click="getTrendingMovies('week')" class="mx-3 h4"
          >This week</a
        >
      </div>

      <div class="row" v-if="movies.length > 0">
        <div class="col-md-3" v-for="(movie, i) in movies" :key="i">
          <movie-card :movie="movie" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"

import MovieCard from "./components/MovieCard.vue";
export default {
  name: "App",
  components: {
    MovieCard,
  },
  data() {
    return {
      movies: [],
      // apiKey: process.env.VUE_APP_API_URL,
      apiKey: 'c2982f33ed20e55f9014dcae5d36a7e0',
    };
  },
  methods: {
   async getTrendingMovies(category) {
    try{

      const response = await axios.get(`https://api.themoviedb.org/3/trending/movie/${category}?api_key=${this.apiKey}`)
      this.movies = response.data.results;
    }catch(err){
      console.error(err);
    }
  },
  },
 async mounted() {
    await this.getTrendingMovies("day");
  },
};
</script>