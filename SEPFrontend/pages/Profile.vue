<template>
  <div class="container">
    <Navbar class="navbar" design="movielist" />
    <div class="heading">
      Profile
    </div>
    <div class="profile-data">
      <div class="profile-picture">
        <img src="../assets/images/spooder.jpg" alt="Profile picture" />
      </div>
      <div class="person">
        <div class="personal-data">
          <div class="profile-item username">
            <h2>Username : {{ user.username }}</h2>
          </div>
          <div class="profile-item name">
            <h2>Name : {{ user.name }}</h2>
          </div>
          <div class="profile-item email">
            <h2>Email : {{ user.email }}</h2>
          </div>
          <div class="profile-item birthday">
            <h2>Birthday : {{ user.birthday }}</h2>
          </div>
          <div class="profile-item country">
            <h2>Country : {{ user.country }}</h2>
          </div>
        </div>
      </div>
    </div>
    <div class="separator">
      <div class="my-list">My List</div>
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

<script>
import Navbar from "../components/Navbar";
export default {
  components: {
    Navbar
  },
  layout: "empty",
  data() {
    return {
      user: {},
      movies: []
    };
  },
  mounted() {
    this.getUser();
  },
  methods: {
    async getUser() {
      var authToken = this.getCookie("authToken");

      await this.$axios
        .get("https://viaucsep6group1.azurewebsites.net/User", {
          headers: {
            fromToken: authToken
          }
        })
        .then(res => {
          this.user = res.data;
          this.movies = this.user.topLists[0].movies;
        });

      this.getImageForMovie();
      console.log(this.movies);
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
  position: relative !important;
}

.container {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  width: 100%;
}

.heading {
  position: relative;
  left: 143px;
  display: block;
  font-size: 2em;
  font-weight: bold;
  margin-bottom: 24px;
}
.profile-data {
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
}
.profile-picture {
  width: 30%;
  right: 76px;
  position: relative;
  img {
    object-fit: fill;
    width: 100%;
    height: 380px;
    border-radius: 180px;
  }
}

.person {
  width: 50%;
  left: 758px;
  top: 148px;
}

.personal-data {
  position: relative;
  border-radius: 5px;
  width: 100%;
  height: 319px;
  display: flex;
  flex-flow: column;
  box-shadow: 0 0 2px 2px #a2a2a224;
}

.profile-item {
  font-size: 14px;
  padding-left: 40px;
}
.styled-break {
  border-top: 1px solid #8c8b8b;
}
.movie-list {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  justify-items: center;
  text-align: center;
  margin-top: 10px;

  .movie {
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: center;
    padding: 22px;
    width: 528px;
    height: 360px;
    box-shadow: 0 0 2px 2px #a2a2a224;
    margin-bottom: 15px;
    position: relative;

    .movie-background {
      width: 100%;
      height: 100%;
      opacity: 0.8;
      position: absolute;
    }

    .overview {
      font-size: 20px;
      font-weight: 600;
      z-index: 2;
      color: rgb(0, 0, 0);
    }
  }
}

.separator {
  width: 100%;
  height: 54px;
  display: flex;
  align-items: center;
  margin-top: 20px;
  margin-bottom: 20px;
  background: #3c3c3c 0% 0% no-repeat padding-box;
}

.my-list {
  position: relative;
  left: 143px;
  color: white;
}

.movie-title {
  padding: 24px;
  font-size: 32px;
  font-weight: 800;
  z-index: 2;
  color: black;
}
</style>
