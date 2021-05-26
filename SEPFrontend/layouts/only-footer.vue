<template>
  <div>
    <client-only>
      <nuxt />
      <Footer />
    </client-only>
  </div>
</template>

<script scoped>
import Footer from "../components/Footer";
export default {
  components: {
    Footer
  }
};
</script>

<style></style>
