<template>
  <!-- Movie Info -->
  <div class="single-movie container">
    <div class="movie-info">
      <div class="movie-img">
        <img
          :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
          alt=""
        />
      </div>
      <div class="movie-content">
        <h1>Title: {{ movie.title }}</h1>
        <p class="movie-fact tagline">
          <span>Tagline:</span> "{{ movie.tagline }}"
        </p>
        <p class="movie-fact">
          <span>Released:</span>
          {{
            new Date(movie.release_date).toLocaleString("en-us", {
              month: "long",
              day: "numeric",
              year: "numeric",
            })
          }}
        </p>
        <p class="movie-fact">
          <span>Duration:</span> {{ movie.runtime }} minutes
        </p>
        <p class="movie-fact">
          <span>Revenue:</span>
          {{
            movie.revenue.toLocaleString("en-us", {
              style: "currency",
              currency: "USD",
            })
          }}
        </p>
        <p class="movie-fact"><span>Overview:</span> {{ movie.overview }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
const { movieId } = useRoute().params;
let movie;

try {
  const data = await axios.get(
    `https://api.themoviedb.org/3/movie/${movieId}?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US`
  );

  movie = data.data;
} catch (error) {
  console.log("error>>", error);
}
</script>

<style lang="scss" scoped>
.single-movie {
  margin-top: 3%;
  color: black;
  width: 100%;
  padding: 32px 16px;
  .movie-info {
    display: grid;
    align-items: center;
    width: 100%;
    gap: 20px;
    color: black;
    grid-template-columns: 1fr;
    @media (min-width: 600px) {
      grid-template-columns: repeat(2, 1fr);
    }
    @media (min-width: 750px) {
      grid-template-columns: repeat(2, 1fr);
    }
    @media (min-width: 1100px) {
      grid-template-columns: repeat(2, 1fr);
    }
    .movie-img {
      img {
        max-height: 500px;
        width: 100%;
        @media (min-width: 800px) {
          max-height: 700px;
          width: auto;
        }
      }
    }
    .movie-content {
      h1 {
        font-size: 40px;
        font-weight: 400;
        font-weight: bold;
        @media (min-width: 800px) {
          font-size: 60px;
        }
      }
      .movie-fact {
        margin-top: 12px;
        font-size: 20px;
        line-height: 1.5;
        span {
          font-weight: 600;
          text-decoration: underline;
        }
      }
      .tagline {
        font-style: italic;
        span {
          font-style: normal;
        }
      }
    }
  }
}
</style>
