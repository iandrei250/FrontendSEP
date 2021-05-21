<template>
  <section>
    <div class="container">
      <div class="overlay"></div>

      <div class="text">Design is the silent ambassador of your brand</div>
      <div class="sub-text">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse a
        consectetur felis. Donec mollis, ligula nec dapibus elementum, nisi
        ligula tincidunt sapien, at tincidunt tellus ex eu enim. Pellentesque
        feugiat aliquam egestas. Duis fringilla urna et quam viverra, consequat
        sodales ex sagittis.
      </div>
      <nuxt-link class="interactive-button" to="#">Contact</nuxt-link>
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
  background-image: url("../assets/images/pepe.jpg");
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
  z-index: 2;
}

.sub-text {
  font-size: 14px;
  text-align: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  padding-bottom: 12px;
  width: 35%;
  z-index: 2;
  color: white;
}

.overlay {
  width: 100%;
  height: 100%;
  position: absolute;
  opacity: 0.3;
  background: rgb(0, 0, 0);
  z-index: 2;
}

.interactive-button {
  z-index: 2;
}
</style>
