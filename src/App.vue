<script>
import axios from "axios";
import MovieResult from "./components/MovieResult.vue";

export default {
  components: {
    MovieResult,
  },
  data() {
    return {
      searchQuery: "",
      movies: [],
    };
  },
  methods: {
    async searchMovies() {
      try {
        const response = await axios.get(
          "https://api.themoviedb.org/3/search/movie?api_key=a78a8b642551188ed870a8264becd909&query=ritorno+al+futuro"
        );
        this.movies = response.data.results;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<template>
  <div class="container mt-4">
    <div class="row justify-content-center">
      <div class="col-lg-6">
        <div class="input-group mb-3">
          <input
            v-model="searchQuery"
            type="text"
            class="form-control"
            placeholder="Cerca film..."
          />
          <button @click="searchMovies" class="btn btn-primary">Cerca</button>
        </div>
      </div>
    </div>
    <div class="row">
      <MovieResult v-for="movie in movies" :key="movie.id" :movie="movie" />
    </div>
  </div>
</template>

<style scoped></style>
