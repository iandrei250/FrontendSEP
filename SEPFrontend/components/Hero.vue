<template>
  <section>
    <div class="container">
      <div class="overlay"></div>
      <div class="video-wrapper">
        <video class="video-background" autoplay muted loop>
          <source
            src="../assets/videos/video wall lighter.mp4"
            type="video/mp4"
          />
        </video>
      </div>
      <div class="text">Bringing Hollywood to your home</div>
      <div class="sub-text">
        Talking about dreams is like talking about movies, since the cinema uses
        the language of dreams; years can pass in a second, and you can hop from
        one place to another. It's a language made of image. And in the real
        cinema, every object and every light means something, as in a dream.
      </div>
    </div>
  </section>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
@import "../assets/style/butons.scss";
.container {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 768px;
  position: relative;
  justify-content: center;
  align-items: center;
  background-repeat: no-repeat;
  background-size: cover;
  cursor: default;
}

.text {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 56px;
  padding-bottom: 12px;
  font-weight: 700;
  white-space: pre;
  color: white;
  z-index: 3;
}

.sub-text {
  font-size: 18px;
  text-align: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  padding-bottom: 12px;
  width: 35%;
  z-index: 3;
  color: white;
}

.overlay {
  width: 100%;
  height: 100%;
  position: absolute;
  opacity: 0.8;
  background: rgb(0, 0, 0);
  z-index: 2;
}

.interactive-button {
  z-index: 2;
}

.video-wrapper {
  position: absolute;
  z-index: 1;
  width: 100%;
  .video-background {
    object-fit: fill;
    height: 768px;
    width: 100%;
    right: 0;
    bottom: 0;
  }
}
</style>
