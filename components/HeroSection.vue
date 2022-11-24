<template>
  <div class="hero">
    <img src="../assets/images/heroBg.jpeg" alt="" />
    <div class="text-container">
      <div class="text">
        <span class="mini-heading">Welcome.</span>
        <h1>
          Millions of movies, TV shows and people to discover. Explore now.
        </h1>
        <!-- <a href="#movie-grid" class="button">View Movies</a> -->
      </div>
      <!-- Search -->
      <div class="container search">
        <input
          type="text"
          placeholder="Search"
          @keyup.enter="
            this.$router.push({
              path: `/search_movie/${searchKey}`,
            })
          "
          v-model.lazy="searchKey"
        />
        <button v-show="searchKey !== ''" @click="clearSearch" class="button">
          Clear Search
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeroSection",
  data() {
    return {
      searchKey: "",
    };
  },

  methods: {
    clearSearch() {
      this.searchKey = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 1400px;
  margin: 0 auto;
}
.hero {
  height: 400px;
  position: relative;
  @media (min-width: 750px) {
    height: 500px;
  }
  &::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.6);
  }
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .text-container {
    z-index: 2;
    position: absolute;
    top: 0;
    margin: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    .text {
      padding: 0 16px;
      width: 100%;
      max-width: 1400px;
      margin: 0 auto;
    }
    .mini-heading {
      font-weight: bold;
      font-size: 44px;
      font-family: "Source Sans Pro", Arial, sans-serif;
      color: #fff;
      margin-bottom: 8px;
      @media (min-width: 750px) {
        font-size: 64px;
      }
    }
    h1 {
      color: #fff;
      font-size: 20px;
      font-weight: 200;
      margin-top: 8px;
      margin-bottom: 8px;
      @media (min-width: 750px) {
        font-size: 25px;
      }
      span {
        font-weight: 500;
      }
    }
  }
  .search {
    display: flex;
    padding: 42px 16px;
    width: 100%;
    input {
      max-width: 350px;
      width: 100%;
      padding: 12px 6px;
      font-size: 14px;
      border-top-left-radius: 10px;
      border-bottom-left-radius: 10px;
      outline: none;
      &:focus {
        outline: none;
      }
    }
    .button {
      border-top-right-radius: 10px;
      border-bottom-right-radius: 10px;
    }
  }
}
</style>
