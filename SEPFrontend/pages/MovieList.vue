<template>
  <div class="container">
    <Navbar class="navbar" design="movielist" />
    <div class="list-container">
      <div class="search-container">
        <div class="searchbar">
          <input type="text" placeholder="Search.." name="search" />
          <button @click="doNothing">
            <div>
              <svg class="svg-icon" viewBox="0 0 20 20">
                <path
                  d="M17.237,3.056H2.93c-0.694,0-1.263,0.568-1.263,1.263v8.837c0,0.694,0.568,1.263,1.263,1.263h4.629v0.879c-0.015,0.086-0.183,0.306-0.273,0.423c-0.223,0.293-0.455,0.592-0.293,0.92c0.07,0.139,0.226,0.303,0.577,0.303h4.819c0.208,0,0.696,0,0.862-0.379c0.162-0.37-0.124-0.682-0.374-0.955c-0.089-0.097-0.231-0.252-0.268-0.328v-0.862h4.629c0.694,0,1.263-0.568,1.263-1.263V4.319C18.5,3.625,17.932,3.056,17.237,3.056 M8.053,16.102C8.232,15.862,8.4,15.597,8.4,15.309v-0.89h3.366v0.89c0,0.303,0.211,0.562,0.419,0.793H8.053z M17.658,13.156c0,0.228-0.193,0.421-0.421,0.421H2.93c-0.228,0-0.421-0.193-0.421-0.421v-1.263h15.149V13.156z M17.658,11.052H2.509V4.319c0-0.228,0.193-0.421,0.421-0.421h14.308c0.228,0,0.421,0.193,0.421,0.421V11.052z"
                ></path>
              </svg>
            </div>
          </button>
        </div>
      </div>
      <div class="header">
        <p>Find your movie</p>
      </div>
      <div class="movie-wrapper">
        <div class="movie" v-for="movie in movies" :key="movie.id">
          <img src="../assets/images/spooder.jpg" alt="Movie image" />
          <div class="movie-title">{{ movie.title }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar";
import axios from "axios";
export default {
  data() {
    return {
      movies: [
        {
          title: "Movie title",
          image: "/assets/images/pepe.jpg"
        },
        {
          title: "Movie title",
          image: "/assets/images/pepe.jpg"
        },
        {
          title: "Movie title",
          image: "/assets/images/pepe.jpg"
        },
        {
          title: "Movie title",
          image: "/assets/images/pepe.jpg"
        },
        {
          title: "Movie title",
          image: "/assets/images/pepe.jpg"
        },
        {
          title: "Movie title",
          image: "/assets/images/pepe.jpg"
        }
      ]
    };
  },
  components: {
    Navbar
  },
  layout: "empty",

  mounted() {
    this.getData();
  },
  methods: {
    doNothing() {
      alert("Hiiiyaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa");
    },

    async getData() {
      var axios = require("axios");
      let data;
      await axios
        .get(
          "https://cors-anywhere.herokuapp.com/https://viaucsep6group1.azurewebsites.net/Movies/mostPopular"
        )
        .then(res => {
          data = res.data;
        });

      // var message = "";

      // movies.forEach(movie => {
      //   message += movie.title + "\n";
      // });

      console.log(data);
    }
  }
};
</script>

<style lang="scss" scoped>
// .overlay {
//   width: 100%;
//   height: 100%;
//   position: absolute;
//   opacity: 0.7;
//   background: rgb(0, 0, 0);
//   z-index: 2;
// }

body {
  padding: 0px !important;
  margin: 0px !important;
  position: absolute;
}
.list-container {
  height: 100% !important;
  width: 100% !important;
  display: flex;
}
.search-container {
  max-height: 100%;
  min-width: 100%;

  position: absolute;
}

.searchbar {
  float: right;
  display: flex;
  box-shadow: 0 0 2px 2px #a2a2a224;
  border-radius: 12px;
  margin: 12px;
}

/* Style the search field */
.searchbar input[type="text"] {
  padding: 10px;
  font-size: 17px;
  border: none;
  width: 500px;
  background: #c5c3c3;
  border-radius: 12px;
  border-top-right-radius: 0px;
  border-bottom-right-radius: 0px;

  &:focus {
    outline: none;
  }
}

/* Style the submit button */
.searchbar button {
  width: 20%;
  padding: 10px;
  background: #2196f3;
  border-radius: 12px;
  color: white;
  font-size: 17px;
  border: none;
  border-left: none; /* Prevent double borders */
  border-top-left-radius: 0px;
  border-bottom-left-radius: 0px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.searchbar button:hover {
  transition: all 0.3s ease;
  background: #0b7dda;
}

.svg-icon {
  height: 15px;
}

.movie-wrapper {
  display: flex;
  flex-wrap: wrap;
  color: white;
  position: relative;
  align-items: center;
  justify-content: space-evenly;
  .movie {
    position: relative;
    top: 15%;
    flex-basis: 34.5%;

    img {
      width: 528px;
      height: 360px;
      object-fit: cover;
    }

    .movie-title {
      color: white;
      top: -230px;
      left: 150px;
      font-size: 36px;
      position: relative;
    }
  }
}

.header {
  position: absolute;
  left: 307px;
  top: 100px;

  p {
    font-family: "Public Sans", sans-serif;
    font-size: 40px;
    font-weight: 600;
  }
}
</style>
