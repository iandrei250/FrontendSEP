<template>
  <div class="container">
    <div class="movie-image">
      <img src="../assets/images/spooder.jpg" alt="Movie image" />
    </div>
  </div>
</template>
<script>
export default {
  layout: "only-navbar"
};
</script>

<style lang="scss">
body {
  margin: 0px !important;
  padding: 0px !important;
}
.container {
  width: 100%;
  height: 100%;
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
</style>
