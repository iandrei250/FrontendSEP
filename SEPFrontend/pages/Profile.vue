<template>
  <div class="container">
    <div class="heading">
      Profile
    </div>
    <div class="profile-data">
      <div class="profile-picture">
        <img src="../assets/images/spooder.jpg" alt="Profile picture" />
      </div>
      <div class="person">
        <div class="personal-data">
          <div class="profile-item username"><h2>Username :</h2></div>
          <div class="profile-item name"><h2>Name :</h2></div>
          <div class="profile-item email"><h2>Email :</h2></div>
          <div class="profile-item birthday"><h2>Birthday :</h2></div>
          <div class="profile-item country"><h2>Country :</h2></div>
        </div>
      </div>
    </div>
    <div class="separator">
      <div class="my-list">My List</div>
    </div>

    <div class="movie-list">
      <div v-for="movie in movies" :key="movie.id" class="movie">
        <div class="movie-title">{{ movie.title }}</div>
        <div>{{ movie.description }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  layout: "empty",
  data() {
    return {
      movies: [
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
    background: url("../assets/images/yoda.jpg");
    color: white;
    margin-bottom: 15px;
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
  font-size: 24px;
  font-weight: 400;
  z-index: 2;
}
</style>
