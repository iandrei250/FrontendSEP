<template>
  <div :design="design">
    <LoginModal ref="login" />
    <RegisterModal ref="register" />
    <nav
      ref="navbar"
      class="navbar"
      role="navigation"
      aria-label="Main navigation"
    >
      <div class="logo-title">
        <img src="../assets/images/logo.png" alt="logo" />
      </div>
      <div class="links" v-if="checkForLoggedInUser() == ``">
        <nuxt-link class="navbar-item" to="/">Home</nuxt-link>
        <nuxt-link class="navbar-item" to="/movielist">Movies</nuxt-link>
      </div>
      <div class="links" v-else>
        <nuxt-link class="navbar-item" to="/">Home</nuxt-link>
        <nuxt-link class="navbar-item" to="/profile">Profile</nuxt-link>
        <nuxt-link class="navbar-item" to="/movielist">Movies</nuxt-link>
      </div>

      <div v-if="checkForLoggedInUser() == ``" class="button-container">
        <div class="auth-btn" @click="openLogin()">
          <button class="interactive-button">Login</button>
        </div>
        <div class="auth-btn" @click="openRegister()">
          <button class="interactive-button">Register</button>
        </div>
      </div>
      <div v-else>
        <div class="auth-btn" @click="logOut()">
          <button class="interactive-button">Log Out</button>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import LoginModal from "../components/LoginModal";
import RegisterModal from "../components/RegisterModal";
export default {
  props: {
    design: {
      validator: prop => ["default", "movielist"].includes(prop),
      default: "default"
    }
  },
  components: {
    LoginModal,
    RegisterModal
  },

  methods: {
    openLogin() {
      this.$refs["login"].open();
    },

    openRegister() {
      this.$refs["register"].open();
    },

    checkForLoggedInUser() {
      var userToken = this.getCookie("authToken");

      return userToken;
    },

    logOut() {
      var token = this.getCookie("authToken");

      this.$axios.post(
        "https://viaucsep6group1.azurewebsites.net/Auth/Logout",
        token
      );

      document.cookie = "authToken=";
      window.location.reload();
    },

    getCookie(name) {
      var dc = document.cookie;
      var prefix = name + "=";
      var begin = dc.indexOf("; " + prefix);
      if (begin == -1) {
        begin = dc.indexOf(prefix);
        if (begin != 0) return null;
      } else {
        begin += 2;
        var end = document.cookie.indexOf(";", begin);
        if (end == -1) {
          end = dc.length;
        }
      }
      // because unescape has been deprecated, replaced with decodeURI
      //return unescape(dc.substring(begin + prefix.length, end));
      return decodeURI(dc.substring(begin + prefix.length, end));
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/style/butons.scss";
nav {
  position: absolute !important;
  z-index: 3;
}
.navbar {
  display: flex;
  min-width: 100%;
  min-height: 80px;
  color: white;
  align-items: center;

  .links {
    padding-left: 24px;
    width: 50% !important;
    height: 100%;
  }

  .auth-btn {
    align-self: right;
    height: 100%;
    margin-right: 12px;
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

  img {
    width: 120px;
    height: 80px;
  }
}
.button-container {
  display: flex;
}

.navbar[design="default"] {
  background-color: transparent !important;
}

.navbar[design="movielist"] {
  background-color: black !important;
}
</style>
