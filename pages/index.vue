<template>
  <div class="home">
    <HeroSection />
    <div class="moviesHeader"><h1>Now Playing</h1></div>
    <!-- Now Streaming  -->
    <div id="movie-grid" class="movies-grid">
      <div class="movie" v-for="(movie, index) in movies" :key="index">
        <div class="movie-img">
          <img
            :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
            alt=""
          />
          <p class="review">{{ movie.vote_average }}</p>
          <p class="overview">{{ movie.overview }}</p>
        </div>
        <div class="info">
          <p class="title">
            {{ movie.title.slice(0, 25)
            }}<span v-if="movie.title.length > 25">...</span>
          </p>
          <p class="release">
            Released:
            {{
              new Date(movie.release_date).toLocaleString("en-us", {
                month: "long",
                day: "numeric",
                year: "numeric",
              })
            }}
          </p>
          <NuxtLink class="button button-light" :to="`/movies/${movie.id}`">
            Get More Info
          </NuxtLink>
        </div>
      </div>
    </div>
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
    .movie-img {
      position: relative;
      overflow: hidden;
      &:hover {
        .overview {
          transform: translateY(0);
        }
      }
      img {
        display: inline-block;
        outline: none;
        width: 100%;
        height: auto;
      }
      .review {
        position: absolute;
        top: 0;
        left: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 40px;
        height: 40px;
        background-color: #013d5b;
        color: #fff;
        border-radius: 0 0 16px 0;
        box-shadow: 0 4px 6px -1px rgba(29, 37, 54, 0.1),
          0 2px 4px -1px rgba(0, 0, 0, 0.06);
      }
      .overview {
        line-height: 1.5;
        position: absolute;
        bottom: 0;
        background-color: rgba(32, 29, 28, 0.9);
        padding: 12px;
        color: #fff;
        transform: translateY(100%);
        transition: 0.3s ease-in-out all;
      }
    }
    .info {
      margin: 20px;
      .title {
        margin-top: 8px;
        color: #fff;
        font-size: 18px;
        font-weight: bold;
      }
      .release {
        margin-top: 8px;
        color: #c9c9c9;
      }
      .button {
        margin-top: 10px;
      }
    }
  }
}
</style>
