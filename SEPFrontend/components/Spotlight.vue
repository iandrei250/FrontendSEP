<template>
  <section>
    <div class="container">
      <div id="spotlight-video">
        <div class="overlay"></div>
        <div class="title">Product spotlight</div>
        <div class="description">
          Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam
          nonumy eirmod tempor invidunt ut.
        </div>
        <div class="play-button">
          <a href="#" class="round-button"><div class="play"></div></a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {};
</script>
<style lang="scss" scoped>
.container {
  width: 100%;
  height: 577px;
  margin-top: 50px;
  background: url("../assets/images/yoda.jpg") 50% 50% no-repeat padding-box;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: default;
}

#spotlight-video {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-flow: column;
  .title {
    text-align: center;
    font-size: 42px;
    font-weight: 700;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    padding: 22px;
    z-index: 3;
    color: white;
  }

  .play-button {
    padding: 22px;
    z-index: 3;
  }

  .round-button {
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 80px;
    height: 80px;
    padding-left: 8px;
    border: 6px solid #fff;
    border-radius: 50%;
    color: #f5f5f5;
    text-decoration: none;
    background-color: rgba(0, 0, 0, 0.5);
    font-size: 20px;
    font-weight: bold;
    transition: all 0.3s ease;
    &:hover {
      transition: all 0.3s ease;
      width: 90px;
      height: 90px;
      background-color: rgba(0, 0, 0, 0.8);
      box-shadow: 0px 0px 10px rgba(255, 255, 100, 1);
      text-shadow: 0px 0px 10px rgba(255, 255, 100, 1);
    }

    .play {
      border-style: solid;
      border-color: white;
      box-sizing: border-box;
      width: 12px;
      height: 12px;
      border-width: 17px 0px 17px 34px;
      border-color: transparent transparent transparent white;
    }
  }

  .description {
    padding: 22px;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    color: white;
    z-index: 3;
  }

  .overlay {
    width: 100%;
    height: 577px;
    position: absolute;
    opacity: 0.3;
    background: rgb(0, 0, 0);
    z-index: 2;
  }
}
</style>
