<template>
  <div class="container">
    <Hero />
    <Featured />
  </div>
</template>

<script>
import Hero from "../components/Hero";
import Featured from "../components/FeaturedProd.vue";
export default {
  components: {
    Hero,
    Featured
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
