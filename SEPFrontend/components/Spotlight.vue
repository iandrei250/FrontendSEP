<template>
  <div class="container">
    <div id="spotlight-video">
      <div class="title">Product spotlight</div>
      <div class="play-button">
        <a href="#" class="round-button"><i class="fas fa-play"></i></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>
<style lang="scss" scoped>
.container {
  width: 100%;
  height: 100%;
  background: gray;
}

#spotlight-video {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-flow: column;
  .title {
    text-align: center;
  }

  .round-button {
    box-sizing: border-box;
    display: block;
    width: 80px;
    height: 80px;
    padding-top: 14px;
    padding-left: 8px;
    line-height: 20px;
    border: 6px solid #fff;
    border-radius: 50%;
    color: #f5f5f5;
    text-align: center;
    text-decoration: none;
    background-color: rgba(0, 0, 0, 0.5);
    font-size: 20px;
    font-weight: bold;
    transition: all 0.3s ease;
  }
  .round-button:hover {
    background-color: rgba(0, 0, 0, 0.8);
    box-shadow: 0px 0px 10px rgba(255, 255, 100, 1);
    text-shadow: 0px 0px 10px rgba(255, 255, 100, 1);
  }
}
</style>
