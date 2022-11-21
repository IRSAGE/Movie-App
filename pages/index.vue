<template>
  <div class="home">
    <HeroSection />
    <div class="moviesHeader"><h1>Now Playing</h1></div>
    <!-- Now Streaming  -->
    <NowStreamingMovie :movies="movies" />
  </div>
</template>

<script setup>
import axios from "axios";

const movies = [];

try {
  const data = await axios.get(
    `https://api.themoviedb.org/3/movie/now_playing?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US&page=1`
  );

  data.data.results.forEach((movie) => {
    movies.push(movie);
  });
} catch (error) {
  console.log("error>>", error);
}
</script>

<style lang="scss">
.moviesHeader {
  margin: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  h1 {
    align-self: center;
  }
}
</style>
