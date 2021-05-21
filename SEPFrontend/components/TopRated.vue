<template>
  <section>
    <div class="container">
      <div class="title">Top Rated Movies</div>
      <div class="top-rated-container">
        <div v-for="movie in topRated" :key="movie.id" class="top-movie">
          <div class="movie-image"></div>
          <div class="overlay"></div>
          <div class="movie-title">{{ movie.title }}</div>
          <div class="movie-description">{{ movie.description }}</div>
          <div class="button-holder">
            <nuxt-link class="interactive-button" to="#">Read More</nuxt-link>
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
      topRated: [
        {
          title: "Movie",
          description:
            "Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna."
        },
        {
          title: "Movie",
          description:
            "Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna."
        },
        {
          title: "Movie",
          description:
            "Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna."
        }
      ]
    };
  }
};
</script>

<style scoped lang="scss">
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
  background: url("../assets/images/spooder.jpg") 50% 70% no-repeat;
  background-size: cover;
  box-shadow: 0 0 4px 4px #52515124;
  border-radius: 8px;
}

.movie-title {
  padding: 24px;
  font-size: 24px;
  font-weight: 400;
  z-index: 2;
}

.movie-description {
  z-index: 2;
  padding: 24px;
  font-weight: 200;
  letter-spacing: 0.5px;
}

.button-holder {
  z-index: 2;
  margin-bottom: auto;
  margin-top: auto;
}

.overlay {
  width: 100%;
  height: 100%;
  position: absolute;
  opacity: 0.3;
  background: rgb(0, 0, 0);
  z-index: 1;
}
</style>
