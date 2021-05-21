<template>
  <div class="container">
    <Hero />
    <Featured />
    <Spotlight />
  </div>
</template>

<script>
import Hero from "../components/Hero";
import Featured from "../components/FeaturedProd.vue";
import Spotlight from "../components/Spotlight.vue";
export default {
  components: {
    Hero,
    Featured,
    Spotlight
  },
  layout: "default"
};
</script>

<style lang="scss">
body {
  margin: 0px !important;
  padding: 0px !important;
}
</style>
