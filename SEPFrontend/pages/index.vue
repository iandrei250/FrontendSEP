<template>
  <div class="container">
    <Hero />
    <PopularMovies />
    <Spotlight />
    <TopRated />
  </div>
</template>

<script>
import Hero from "../components/Hero.vue";
import PopularMovies from "../components/PopularMovies.vue";
import Spotlight from "../components/Spotlight.vue";
import TopRated from "../components/TopRated.vue";
export default {
  components: {
    Hero,
    PopularMovies,
    Spotlight,
    TopRated
  },
  mounted() {
    this.getData();
  },
  methods: {
    async getData() {
      var axios = require("axios");
      let data;
      await axios
        .get("https://viaucsep6group1.azurewebsites.net/Movies/mostPopular")
        .then(res => {
          data = res.data;
        });

      // var message = "";

      // movies.forEach(movie => {
      //   message += movie.title + "\n";
      // });

      console.log(data);
    }
  },
  layout: "default"
};
</script>

<style lang="scss">
html {
  overflow: scroll;
  overflow-x: hidden;
}
::-webkit-scrollbar {
  width: 0; /* Remove scrollbar space */
  background: transparent; /* Optional: just make scrollbar invisible */
}
body {
  margin: 0px !important;
  padding: 0px !important;
  position: relative;
}
</style>
