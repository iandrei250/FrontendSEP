<template>
  <section>
    <div class="container">
      <div class="featured-title">Popular Movies</div>
      <div class="featured-container">
        <div
          id="featured-solutions"
          v-for="movie in popularMovies"
          :key="movie.key"
        >
          <div class="image-holder">
            <div class="image">
              <nuxt-link
                class="overlay"
                :to="`/movie?movie=${movie.id}`"
              ></nuxt-link>
              <img
                :src="
                  `http://image.tmdb.org/t/p/original/${movie.backdrop_path}`
                "
                alt="featured image"
              />
            </div>
          </div>
          <div class="item-info-holder">
            <div class="title-text">{{ movie.title }}</div>
            <div class="description">{{ movie.overview }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      popularMovies: []
    };
  },

  mounted() {
    this.getData();
    this.deleteSearch();
  },

  methods: {
    async getData() {
      let movie;
      await this.$axios
        .get("https://viaucsep6group1.azurewebsites.net/Movies/mostPopular")
        .then(res => {
          for (let i = 1; i <= 3; i++) {
            if (this.popularMovies.length === 3) break;
            movie = res.data[Math.floor(Math.random() * res.data.length)];
            if (this.popularMovies.indexOf(movie) < 0) {
              this.popularMovies.push(movie);
            } else {
              i = 1;
            }
          }
        });
    },
    deleteSearch() {
      document.cookie = "search= ; expires = Thu, 01 Jan 1970 00:00:00 GMT";
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/style/butons.scss";

.container {
  width: 100%;
  margin-top: 50px;
  cursor: default;
}

.featured-container {
  display: flex;
  align-content: center;
  justify-content: center;
}

.featured-title {
  text-align: center;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 42px;
  font-weight: 600;
  padding: 22px;
  margin-top: 50px;
}

#featured-solutions {
  // border: 1px solid black;
  position: relative;
  border-radius: 10px;
  display: flex;
  flex-flow: column;
  margin: 22px;
  width: 25%;
  height: 100%;
  background: white;
  box-shadow: 0 0 2px 2px #a2a2a224;

  .title-text {
    text-align: center;
    display: block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    padding: 8px;
    font-size: 24px;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
  }

  .description {
    display: block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: center;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-size: 12px;
    padding: 0 22px 22px 22px;
  }

  .read-more {
    align-self: center;
    padding-bottom: 22px;
  }
}

.image-holder {
  width: 100%;
  height: 50%;

  .image {
    .overlay {
      position: absolute;
      width: 100%;
      height: 100%;
      background: black;
      opacity: 0;
      transition: all 0.3s ease;
    }
    &:hover {
      .overlay {
        opacity: 0.3;
        transition: all 0.3s ease;
        z-index: 999;
      }
    }
    img {
      width: 100% !important;
      height: 325px !important;
      border-top-left-radius: 10px;
      border-top-right-radius: 10px;
      object-fit: fill;
    }
  }
}

.item-info-holder {
  display: flex;
  flex-flow: column;
  justify-content: center;
  width: 100%;
  height: 50%;
}
</style>
