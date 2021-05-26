<template>
  <div>
    <LoginModal ref="login" />
    <RegisterModal ref="register" />
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
      <div class="login-btn" @click="openLogin()">
        <nuxt-link class="interactive-button" to="#">Login</nuxt-link>
      </div>
      <div class="login-btn" @click="openRegister()">
        <nuxt-link class="interactive-button" to="#">Register</nuxt-link>
      </div>
    </nav>
  </div>
</template>

<script>
import LoginModal from "../components/LoginModal";
import RegisterModal from "../components/RegisterModal";
export default {
  components: {
    LoginModal,
    RegisterModal
  },

  methods: {
    openLogin() {
      this.$refs["login"].open();
      this.$refs["register"].close();
    },

    openRegister() {
      this.$refs["register"].open();
      this.$refs["login"].close();
    }
  }
};
</script>

<style lang="scss">
@import "../assets/style/butons.scss";
nav {
  position: absolute !important;
  z-index: 3;
}
.navbar {
  display: flex;
  min-width: 100%;
  min-height: 80px;
  background-color: transparent;
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
  position: relative;
  transition: all 0.3s ease;
  margin: 8px 12px;
  font-size: 22px;
  color: white;
  text-decoration: none;

  &:hover {
    transition: all 0.3s ease;
    font-size: 26px;
    color: rgb(202, 80, 23);
  }
}

.logo-title {
  text-align: center;
  font-size: 24px;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  width: 25%;
  height: 100%;
  cursor: default;
}
</style>
