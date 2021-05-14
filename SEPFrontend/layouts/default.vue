<template>
  <div>
    <client-only>
      <Navbar />
      <nuxt />
      <Footer />
    </client-only>
  </div>
</template>

<script>
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
