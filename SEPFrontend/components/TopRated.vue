<template>
  <section>
    <div class="container">
      <div class="title">Top Rated Movies</div>
      <div class="top-rated-container">
        <div v-for="movie in topRated" :key="movie.id" class="top-movie">
          <div class="movie-image">
            <nuxt-link
              class="overlay"
              :to="`/movie?movie=${movie.imdb_id}`"
            ></nuxt-link>
            <img
              class="image"
              :src="`http://image.tmdb.org/t/p/original/${movie.backdrop_path}`"
              alt="Movie image"
            />
          </div>

          <div class="movie-title">{{ movie.title }}</div>
          <div class="movie-description">{{ movie.overview }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      topRated: []
    };
  },
  mounted() {
    this.getData();
  },

  methods: {
    async getData() {
      let movie;
      await this.$axios
        .get("https://viaucsep6group1.azurewebsites.net/Movies/topRated")
        .then(res => {
          for (let i = 1; i <= 3; i++) {
            movie = res.data[Math.floor(Math.random() * res.data.length)];

            this.topRated.push(movie);
          }
        });
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/style/butons.scss";
section {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
.container {
  width: 100%;
  height: 616px;
  cursor: default;
}

.title {
  font-size: 42px;
  font-weight: 700;
  padding: 22px;
  text-align: center;
  margin-top: 50px;
}

.top-rated-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.top-movie {
  position: relative;
  margin: 22px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-flow: column;
  text-align: center;
  color: white;
  border: 1px solid black;
  height: 323px;
  width: 25%;
  background-size: cover;
  box-shadow: 0 0 4px 4px #52515124;
  border-radius: 8px;
}

.movie-title {
  margin-top: 25px;
  font-size: 24px;
  font-weight: 400;
  z-index: 2;
  color: white;
}

.movie-description {
  z-index: 2;
  padding: 24px;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.movie-image {
  position: absolute;
  height: 100%;

  .image {
    position: relative;
  }

  .overlay {
    width: 100%;
    height: 100%;
    position: absolute;
    opacity: 0;
    background: rgb(0, 0, 0);
    z-index: 1;
  }

  &:hover {
    .overlay {
      position: absolute;
      opacity: 0.3;
      transition: all 0.3s ease;
      z-index: 999;
    }
  }
}
</style>
