<template>
  <div class="container">
    <div class="movie-image">
      <img
        v-if="movie.backdrop_path != null"
        :src="`http://image.tmdb.org/t/p/original/${movie.backdrop_path}`"
        alt="Movie image"
      />
      <img
        v-else
        src="../assets/images/No_Image_Available.jpg"
        alt="Movie image"
      />
      <button
        class="interactive-button"
        id="favourite"
        @click="addToTopLists()"
      >
        Add to favourite
      </button>
    </div>
    <div class="movie-header">
      <div class="title">{{ this.movie.title }}</div>
    </div>
    <div class="movie-overview">
      <div class="overview-text">
        {{ this.movie.overview }}
      </div>
    </div>
    <div class="release-date">
      Release date : {{ formatDate(movie.release_date) }}
    </div>
    <div class="ratings-container">
      <div class="svg-icon">
        <div class="icon">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
          >
            <path
              d="M17.867 3.493l4.133 3.444v5.127l-10 8.333-10-8.334v-5.126l4.133-3.444 5.867 3.911 5.867-3.911zm.133-2.493l-6 4-6-4-6 5v7l12 10 12-10v-7l-6-5z"
            />
          </svg>
        </div>
      </div>
      <div class="ratings">Rating: {{ movie.vote_average }}/10</div>
    </div>
    <div class="amount">Amount of votes: {{ movie.vote_count }}</div>
    <hr class="line-separator" />
    <div class="cast">
      <div class="cast-header">Cast :</div>
      <div class="cast-container">
        <div v-if="actors.length == 0" class="no-data">
          No data found to display
        </div>
        <div v-else class="actor" v-for="actor in actors" :key="actor.key">
          <div class="actor-image" v-if="actors.length != 0">
            <img
              v-if="actors.length != 0 || actors.profile_path != null"
              :src="`http://image.tmdb.org/t/p/original/${actor.profile_path}`"
              alt="Actor profile image"
            />
            <img
              v-else
              src="../assets/images/No_Image_Available.jpg"
              alt="Actor profile image"
            />
          </div>
          <div class="actor-name">{{ actor.name }}</div>
        </div>
      </div>

      <div class="directors-header">Directors:</div>
      <div class="directors-container">
        <div v-if="directors.length == 0" class="no-data">
          No data found to display
        </div>
        <div
          v-else
          class="director"
          v-for="director in directors"
          :key="director.key"
        >
          <div class="director-image">
            <img
              v-if="directors.length == 0 || director.profile_path == null"
              src="../assets/images/No_Image_Available.jpg"
              alt="Director profile image"
            />

            <img
              v-else
              :src="
                `http://image.tmdb.org/t/p/original/${director.profile_path}`
              "
              alt="Director profile image"
            />
          </div>
          <div class="director-name">{{ director.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      movieId: 0,
      movie: {},
      actors: [],
      directors: [],
      movies: []
    };
  },
  layout: "only-navbar",
  mounted() {
    this.getMovieData();
    this.getDirectors();
    this.getActors();
    this.checkForAuthToFavourite();
    console.log(this.directors);
  },

  methods: {
    async getMovieData() {
      var cookie = this.getCookie("search");
      this.movieId = this.$route.query.movie;
      console.log(this.movieId);
      if (cookie === null) {
        await this.$axios
          .get("https://viaucsep6group1.azurewebsites.net/Movies/mostPopular")
          .then(res => {
            res.data.forEach(element => {
              if (this.movieId == element.id) {
                this.movie = element;
                console.log(this.movie.id);
              }
            });
          });
      } else {
        this.$axios
          .get(
            `https://viaucsep6group1.azurewebsites.net/Movies?id=${this.movieId}`
          )
          .then(res => {
            if (res.data.tmdbMovie == null) {
              this.movie = res.data.movie;
            } else if (res.data.tmdbMovie != null) {
              this.movie = res.data.tmdbMovie;
            }
          });
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
    },

    formatDate(date) {
      var dateToDisplay = new Date(date);
      return dateToDisplay.toUTCString();
    },

    async getDirectors() {
      try {
        this.$axios
          .get(
            `https://viaucsep6group1.azurewebsites.net/Movies/directors?id=${this.movieId}`
          )
          .then(res => {
            this.directors = res.data;
          });
      } catch (e) {
        console.log(e.message);
      }
    },

    async getActors() {
      this.$axios
        .get(
          `https://viaucsep6group1.azurewebsites.net/Movies/stars?id=${this.movieId}`
        )
        .then(res => {
          this.actors = res.data;
        });

      console.log(this.actors);
    },

    checkForAuthToFavourite() {
      var auth = this.getCookie("authToken");

      if (auth != "") {
        console.log(auth);
        document.getElementById("favourite").classList.add("is-active");
      }
    },

    async addToTopLists() {
      var token = this.getCookie("authToken");

      if (token.includes(";")) {
        token = token.split("; ")[0];
      }

      var id = token.split("=")[0];

      let movie = {
        id: this.movieId,
        title: "",
        year: 0
      };

      this.movies.push(this.movie);

      var topListOption = {
        id: 0,
        name: "My list",
        userId: id,
        movies: []
      };

      try {
        let userWithData = {};

        await this.$axios
          .get(`https://viaucsep6group1.azurewebsites.net/User`, {
            headers: { fromToken: token }
          })
          .then(res => {
            userWithData = res.data;
          });

        if (userWithData.topLists.length == 0) {
          topListOption.movies = this.movies;
          var res = await this.$axios.post(
            `https://viaucsep6group1.azurewebsites.net/Toplists`,
            topListOption,
            {
              headers: {
                token: token
              }
            }
          );
          alert(res.data);
        } else {
          userWithData.topLists.forEach(async topList => {
            if (topList.name == topListOption.name) {
              topListOption.id = topList.id;
              this.movie.id = parseInt(this.movieId);
              topList.movies.push(this.movie);
              topListOption.movies = topList.movies;
              console.log(topListOption);

              var res = await this.$axios.put(
                `https://viaucsep6group1.azurewebsites.net/Toplists`,
                topListOption,
                { headers: { token: token } }
              );

              alert(res.data);
            } else {
              var res = await this.$axios.post(
                `https://viaucsep6group1.azurewebsites.net/Toplists`,
                topListOption,
                {
                  headers: {
                    token: token
                  }
                }
              );
              alert(res.data);
              console.log(res.data);
            }
          });
        }
      } catch (e) {
        console.log(e.message);
      }
    }
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web:wght@300&display=swap");
@import "../assets/style/butons.scss";
body {
  margin: 0px !important;
  padding: 0px !important;
}
.container {
  width: 100%;
  height: 100%;
  font-family: "Titillium Web", sans-serif;
}
.movie-image {
  width: 100%;
  height: 600px;
  position: relative;

  .interactive-button {
    z-index: 99;
    position: absolute;
    width: 200px;
    bottom: 0;
    visibility: hidden;
    right: 0;
    border-radius: 42px;
    margin: 10px;

    background: transparent;
    border: 2px solid rgb(172, 45, 45);

    &:hover {
      background: rgb(172, 45, 45);
    }

    &.is-active {
      visibility: visible;
    }
  }
  img {
    z-index: 1;
    position: absolute;
    width: 100%;
    height: 100%;
    object-fit: fill;
  }
}
.movie-header {
  width: 100%;
  padding: 12px;
  .category {
    position: relative;
    left: 307px;
    font-size: 16px;
    font-weight: bold;
  }

  .title {
    position: relative;
    left: 307px;
    font-size: 40px;
    font-weight: 700;
    letter-spacing: 1px;
  }
}

.movie-overview {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;

  .overview-text {
    font-size: 32px;
    width: 50%;
    letter-spacing: 0px;
    text-align: justify;
  }
}

.ratings-container {
  width: 100%;
  display: flex;
  position: relative;
  align-items: center;
  left: 307px;
  margin-bottom: 10px;

  .svg-icon {
    margin-right: 12px;
    width: 25px;
    height: 25px;
    border: 2px solid black;
    padding: 10px;
    padding-bottom: 5px;
    border-radius: 50%;
    z-index: 1;
    position: relative;
    svg {
      z-index: 2;
      background: transparent;
    }
  }

  .ratings {
    font-size: 21px;
    text-align: justify;
    top: 10px;
  }
}

.amount {
  position: relative;
  left: 307px;
  margin-top: 20px;
  margin-bottom: 20px;
  font-size: 21px;
}

.line-separator {
  border: 1px solid rgb(83, 83, 83);
  width: 70%;
}

.cast {
  width: 100%;
  position: relative;
  left: 307px;

  .cast-header {
    margin-bottom: 12px;
    font-size: 40px;
    font-weight: 550;
    letter-spacing: 1px;
  }
}

.cast-container {
  display: flex;
  flex-wrap: wrap;

  .actor {
    display: flex;
    margin: 12px;
    flex-basis: 27.5%;
    .actor-image {
      align-self: center;
      img {
        width: 100px;
        height: 100px;
        border-radius: 50%;
      }
    }

    .actor-name {
      align-self: center;
      margin-left: 20px;
      font-size: 20px;
      font-weight: 600;
    }
  }
}

.directors-container {
  display: flex;
  flex-wrap: wrap;
  .director {
    display: flex;
    margin: 12px;
    flex-basis: 27.5%;
    .director-image {
      align-self: center;
      img {
        width: 100px;
        height: 100px;
        border-radius: 50%;
      }
    }

    .director-name {
      align-self: center;
      margin-left: 20px;
      font-size: 20px;
      font-weight: 600;
    }
  }
}
.directors-header {
  margin-bottom: 12px;
  font-size: 40px;
  font-weight: 550;
  letter-spacing: 1px;
}

.release-date {
  width: 100%;
  display: flex;
  position: relative;
  align-items: center;
  left: 307px;
  margin-top: 20px;
  margin-bottom: 30px;
  font-weight: 550;
  font-size: 21px;
  text-align: justify;
  top: 10px;
}
.no-data {
  margin-top: 20px;
  margin-bottom: 20px;
  padding-left: 12px;
  font-size: 24px;
}
</style>
