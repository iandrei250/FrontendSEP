<template>
  <nav
    ref="navbar"
    class="navbar"
    role="navigation"
    aria-label="Main navigation"
  >
    <div class="logo-title">Logo and title</div>
    <div class="links">
      <nuxt-link class="navbar-item" to="#">Home</nuxt-link>
      <nuxt-link class="navbar-item" to="#">About us</nuxt-link>
      <nuxt-link class="navbar-item" to="#">Contact</nuxt-link>
      <nuxt-link class="navbar-item" to="#">Register</nuxt-link>
    </div>
    <div class="login-btn">
      <nuxt-link class="interactive-button" to="#">Login</nuxt-link>
    </div>
  </nav>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
@import "../assets/style/butons.scss";
.navbar {
  display: flex;
  min-width: 100%;
  min-height: 80px;
  background-color: rgb(17, 16, 16);
  color: white;
  align-items: center;

  .links {
    padding-left: 24px;
    width: 50% !important;
    height: 100%;
  }

  .login-btn {
    align-self: right;
    width: 25%;
    height: 100%;
    display: flex;
    justify-content: center;
  }
}

.navbar-item {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  margin: 8px 12px;
  font-size: 24px;
  color: white;
  text-decoration: none;

  &:hover {
    border-bottom: 2px solid rgb(57, 143, 57);
  }
}

.logo-title {
  text-align: center;
  font-size: 24px;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  width: 25%;
  height: 100%;
}
</style>
