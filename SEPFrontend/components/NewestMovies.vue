<template>
  <section>
    <div class="container">
      <div class="featured-title">Newest Movies</div>
      <div class="featured-container">
        <div
          id="featured-solutions"
          v-for="solution in solutions"
          :key="solution.key"
        >
          <div class="image-holder">
            <div class="image">
              <img src="../assets/images/pepe.jpg" alt="featured image" />
            </div>
          </div>
          <div class="item-info-holder">
            <div class="title-text">{{ solution.title }}</div>
            <div class="description">{{ solution.description }}</div>
            <div class="read-more">
              <nuxt-link class="interactive-button" to="#">Read More</nuxt-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      solutions: [
        {
          title: "Lorem Ipsum Dolor",
          description:
            " Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse a consectetur felis. Donec mollis, ligula nec dapibus elementum, nisi ligula tincidunt sapien, at tincidunt tellus ex eu enim. Pellentesque feugiat aliquam egestas"
        },
        {
          title: "Lorem Ipsum Dolor",
          description:
            " Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse a consectetur felis. Donec mollis, ligula nec dapibus elementum, nisi ligula tincidunt sapien, at tincidunt tellus ex eu enim. Pellentesque feugiat aliquam egestas"
        },
        {
          title: "Lorem Ipsum Dolor",
          description:
            " Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse a consectetur felis. Donec mollis, ligula nec dapibus elementum, nisi ligula tincidunt sapien, at tincidunt tellus ex eu enim. Pellentesque feugiat aliquam egestas"
        }
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/style/butons.scss";

.container {
  width: 100%;
  margin-top: 50px;
  cursor: default;
}

.featured-container {
  display: flex;
  align-content: center;
  justify-content: center;
}

.featured-title {
  text-align: center;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 42px;
  font-weight: 700;
  padding: 22px;
}

#featured-solutions {
  // border: 1px solid black;
  border-radius: 10px;
  display: flex;
  flex-flow: column;
  margin: 22px;
  width: 25%;
  height: 100%;
  background: white;
  box-shadow: 0 0 2px 2px #a2a2a224;

  .title-text {
    text-align: center;
    padding: 8px;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
  }

  .description {
    text-align: center;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-size: 12px;
    padding: 0 22px 22px 22px;
  }

  .read-more {
    align-self: center;
    padding-bottom: 22px;
  }
}

.image-holder {
  width: 100%;
  height: 50%;

  .image {
    img {
      width: 100% !important;
      height: 325px !important;
      border-top-left-radius: 10px;
      border-top-right-radius: 10px;
      object-fit: fill;
    }
  }
}

.item-info-holder {
  display: flex;
  flex-flow: column;
  justify-content: center;
  width: 100%;
  height: 50%;
}
</style>
