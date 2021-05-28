<template>
  <div class="container">
    <Hero />
    <NewestMovies />
    <Spotlight />
    <TopRated />
  </div>
</template>

<script>
import Hero from "../components/Hero.vue";
import NewestMovies from "../components/NewestMovies.vue";
import Spotlight from "../components/Spotlight.vue";
import TopRated from "../components/TopRated.vue";
export default {
  components: {
    Hero,
    NewestMovies,
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
