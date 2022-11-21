<template>
  <div id="movie-grid" class="movies-grid">
    <div class="movie" v-for="(movie, index) in movies" :key="index">
      <MovieComp :movie="movie" />
    </div>
  </div>
</template>

<script>
export default {
  name: "NowStreamingMovie",
  props: ["movies"],
};
</script>

<style lang="scss">
.movies-grid {
  display: grid;
  column-gap: 40px;
  row-gap: 64px;
  margin: 25px;
  grid-template-columns: 1fr;
  @media (min-width: 500px) {
    grid-template-columns: repeat(2, 1fr);
  }
  @media (min-width: 750px) {
    grid-template-columns: repeat(3, 1fr);
  }
  @media (min-width: 1100px) {
    grid-template-columns: repeat(4, 1fr);
  }
  .movie {
    position: relative;
    display: flex;
    flex-direction: column;
    background-color: #013d5b;
    border-radius: 15px;
    height: 500px;
  }
}
</style>
