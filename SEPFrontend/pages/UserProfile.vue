<template>
  <div>
    <Navbar class="navbar" design="movielist" />
    <div class="heading">{{ user.username }}'s Profile</div>
    <div class="profile-data">
      <div class="profile-picture">
        <img
          src="../assets/images/No_Image_Available.jpg"
          alt="Profile picture"
        />
      </div>
      <div class="person">
        <div class="user-data">
          <div class="profile-item username">
            <h2>Username : {{ user.username }}</h2>
          </div>
          <div class="profile-item email">
            <h2>Email : {{ user.email }}</h2>
          </div>
          <div class="profile-item country">
            <h2>Country : {{ user.country }}</h2>
          </div>
        </div>
      </div>
    </div>
    <div class="separator">
      <div class="my-list">{{ user.username }}'s List</div>
    </div>
    <div class="movie-list">
      <div v-for="movie in movies" :key="movie.id" class="movie">
        <img
          v-if="movie.backdrop_path == null"
          class="movie-background"
          src="../assets/images/No_Image_Available.jpg"
          alt="movie image"
        />
        <img
          v-else
          class="movie-background"
          :src="`http://image.tmdb.org/t/p/original/${movie.backdrop_path}`"
          alt="movie image"
        />
        <div class="movie-title">{{ movie.title }}</div>
        <div class="overview">{{ movie.overview }}</div>
      </div>
    </div>
  </div>
</template>

<script scoped>
import Navbar from "../components/Navbar";
export default {
  data() {
    return {
      userName: "",
      user: {},
      movies: []
    };
  },
  components: {
    Navbar
  },
  layout: "empty",
  mounted() {
    this.getUser();
    this.getMovies();
    console.log(this.userId);
  },

  methods: {
    async getUser() {
      this.userName = this.$route.query.user;
      var token = this.getCookie("authToken");

      if (token.includes(";")) {
        token = token.split("; ")[0];
      }
      console.log(token);

      await this.$axios
        .get(
          `https://viaucsep6group1.azurewebsites.net/User?toUser=${this.userName}`,
          {
            headers: {
              fromToken: token
            }
          }
        )
        .then(res => {
          this.user = res.data;
        });
    },

    async getMovies() {
      this.userName = this.$route.query.user;
      var token = this.getCookie("authToken");

      if (token.includes(";")) {
        token = token.split("; ")[0];
      }

      await this.$axios
        .get(
          `https://viaucsep6group1.azurewebsites.net/User?toUser=${this.userName}`,
          {
            headers: {
              fromToken: token
            }
          }
        )
        .then(res => {
          this.movies = this.user.topLists[0].movies;
          this.getImageForMovie();
        });
    },

    async getImageForMovie() {
      let dataToLoad;
      for (let i = 0; i < this.movies.length; i++) {
        await this.$axios
          .get(
            `https://viaucsep6group1.azurewebsites.net/Movies?id=${this.movies[i].id}`
          )
          .then(res => {
            dataToLoad = res.data;
          });
        if (dataToLoad.tmdbMovie == null) {
          this.movies[i].backdop_path = null;
        } else {
          this.movies[i].backdrop_path = dataToLoad.tmdbMovie.backdrop_path;
          this.movies[i].overview = dataToLoad.tmdbMovie.overview;
        }

        console.log(this.movies[i].overview);
      }
    },
    getCookie(name) {
      var dc = document.cookie;
      var prefix = name + "=";
      var begin = dc.indexOf("; " + prefix);
      if (begin == -1) {
        begin = dc.indexOf(prefix);
        if (begin != 0) return null;
      } else {
        begin += 2;
        var end = document.cookie.indexOf(";", begin);
        if (end == -1) {
          end = dc.length;
        }
      }
      // because unescape has been deprecated, replaced with decodeURI
      //return unescape(dc.substring(begin + prefix.length, end));
      return decodeURI(dc.substring(begin + prefix.length, end));
    }
  }
};
</script>

<style lang="scss">
div {
  font-family: Arial, Helvetica, sans-serif;
}
.user-data {
  position: relative;
  border-radius: 5px;
  width: 100%;
  height: 219px;
  display: flex;
  flex-flow: column;
  box-shadow: 0 0 2px 2px #a2a2a224;
  justify-content: center;
}
</style>
