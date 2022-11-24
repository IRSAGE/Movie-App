<template>
  <HeroSection />
  <div v-if="searchedMovies.length != 0" class="searchedmoviesgrid">
    <h1>Found ({{ searchedMovies.length }}) Movies</h1>
    <div class="movies" v-for="(movie, index) in searchedMovies" :key="index">
      <NuxtLink class="movie" :to="`/movies/${movie.id}`">
        <div class="movie-img">
          <img
            v-if="movie.poster_path != null"
            :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
            alt=""
          />
          <img
            v-else
            :src="`https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrTSx2hLlMDpo_1q7XvbVmKzWVMWWo5X_FoQ&usqp=CAU`"
            alt=""
          />
        </div>
        <div class="info">
          <p class="title">{{ movie.title }}</p>
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
          <p v-if="movie.overview.length != 0" class="overview">
            {{ movie.overview.slice(0, 500)
            }}<span v-if="movie.overview.length > 500">...</span>
          </p>
          <p v-else class="overview">.......</p>
        </div>
      </NuxtLink>
    </div>
  </div>
  <div v-else class="notFound">
    <img
      :src="`https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrTSx2hLlMDpo_1q7XvbVmKzWVMWWo5X_FoQ&usqp=CAU`"
      alt=""
    />
    <p>No movie found! for "{{ searchKey }}"</p>
  </div>
</template>

<script setup>
import axios from "axios";
const { searchKey } = useRoute().params;
const searchedMovies = [];
try {
  const data = await axios.get(
    `https://api.themoviedb.org/3/search/movie?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US&page=1&query=${searchKey}`
  );

  data.data.results.forEach((movie) => {
    searchedMovies.push(movie);
  });
} catch (error) {
  console.log("error>>", error);
}
</script>

<style lang="scss" scoped>
.searchedmoviesgrid {
  margin: 5%;
  justify-content: center;
  align-items: center;

  h1 {
    margin-bottom: 4%;
  }
  .movies {
    .movie {
      text-decoration: none;
      color: black;
      display: grid;
      grid-template-columns: 80px auto;
      grid-gap: 1.3rem;
      margin: 2rem 0;
      box-shadow: 0 0 20px rgb(0 0 0 / 5%);
      border: 1px solid #ccc;
      @media (max-width: 600px) {
        grid-template-columns: repeat(1, 1fr);
        .movie-img {
          height: 80px;
        }
      }
      .movie-img {
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        position: relative;
        overflow: hidden;
        img {
          display: inline-block;
          outline: none;
          width: 100%;
          height: auto;
        }
      }
      .info {
        margin-top: 5px;
        .title {
          font-size: 20px;
          font-weight: bold;
          margin-bottom: 5px;
        }
        .release {
          color: gray;
          font-size: 16px;
          margin-bottom: 10px;
        }
        .overview {
          color: gray;
          font-size: 14px;
          margin-bottom: 5px;
        }
      }
    }
  }
}
.notFound {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 5%;
  img {
    height: 10%;
  }
  p {
    font-size: 30px;
    font-weight: bold;
  }
}
</style>
