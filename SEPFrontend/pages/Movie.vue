<template>
  <div class="container">
    <div class="movie-image">
      <img src="../assets/images/spooder.jpg" alt="Movie image" />
    </div>
    <div class="movie-header">
      <div class="category">Movie Category</div>
      <div class="title">Movie Title</div>
    </div>
    <div class="movie-overview">
      <div class="overview-text">
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Aut doloremque
        necessitatibus, fuga asperiores doloribus dolorem odio obcaecati error
        reiciendis neque soluta rerum ad similique consequatur quam. Explicabo,
        voluptate necessitatibus corrupti tempore vero a animi. Expedita illo
        labore, eum, quis illum fugiat, in consequatur laudantium totam dolores
        magnam ut quisquam nihil.
      </div>
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
      <div class="ratings">Rating:</div>
    </div>
    <hr class="line-separator" />
    <div class="cast">
      <div class="cast-header">Cast :</div>
      <div class="cast-container">
        <div class="actor" v-for="actor in actors" :key="actor.key">
          <div class="actor-image">
            <img src="../assets/images/pepe.jpg" alt="Actor profile image" />
          </div>
          <div class="actor-name">{{ actor.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      actors: [
        {
          name: "Actor name",
          image: "Actor image"
        }
      ]
    };
  },
  layout: "only-navbar"
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web:wght@300&display=swap");
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
  img {
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
    font-size: 40px;
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
    border: 2px solid black;
    padding: 10px;
    padding-bottom: 1px;
    border-radius: 100%;
    z-index: 1;
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
  width: 100%;
  display: flex;

  .actor {
    display: flex;
    flex-flow: column;
    align-items: center;
    .actor-image {
      img {
        width: 100px;
        height: 100px;
        border-radius: 50%;
      }
    }
  }
}
</style>
