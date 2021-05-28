<template>
  <div>
    <client-only>
      <Navbar design="default" />
      <nuxt />
      <Footer />
    </client-only>
  </div>
</template>

<script scoped>
import Navbar from "../components/Navbar";
import Footer from "../components/Footer";
export default {
  components: {
    Navbar,
    Footer
  }
};
</script>

<style></style>
