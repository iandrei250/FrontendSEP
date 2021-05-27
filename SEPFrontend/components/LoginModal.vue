<template>
  <div class="container">
    <transition name="fade" appear>
      <div class="modal-overlay" v-if="showModal" @click="close"></div>
    </transition>
    <transition name="slide" appear>
      <div class="modal" v-if="showModal">
        <div class="first-half">
          <h1>Sign In</h1>
          <div class="login-form">
            <input
              type="text"
              id="username"
              name="username"
              placeholder="Username"
              ref="username"
            />
            <input
              type="password"
              id="password"
              name="password"
              placeholder="Password"
              ref="password"
            />
            <div class="buttons-container">
              <button class="button" @click="login">
                Log In
              </button>
              <button class="button" @click="close">
                Cancel
              </button>
            </div>
          </div>
        </div>
        <div class="second-half">
          <div class="login-icon">
            <img src="../assets/images/Forms/LoginIcon.png" alt="Login Icon" />
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showModal: false
    };
  },
  methods: {
    open() {
      this.showModal = true;
      const x = window.scrollX;
      const y = window.scrollY;
      window.onscroll = function() {
        window.scrollTo(x, y);
      };
    },
    close() {
      this.showModal = false;
      window.onscroll = function() {};
    },

    login() {
      var user = document.getElementById("username").value;
      var pass = document.getElementById("password").value;
      alert(user + "\n" + pass);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/style/butons.scss";
.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 998;
  background-color: rgba(0, 0, 0, 0.3);
}

.modal {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 999;
  display: flex;

  width: 695px;
  height: 373px;
  background-color: #fff;
  border-radius: 16px;

  padding: 25px;

  h1 {
    color: #222;
    font-size: 42px;
    font-weight: 900;
    margin-bottom: 15px;
    padding-left: 20px;
  }

  .login-form {
    display: flex;
    flex-flow: column;

    input {
      margin: 8px;
      height: 48px;
      border: 2px solid #3e3e3e;
      text-align: left;
      padding-left: 22px;
      border-radius: 11px;
    }
  }
}

.first-half {
  width: 50%;
  align-self: center;
}

.second-half {
  width: 50%;
  align-self: center;
  .login-icon {
    display: flex;
    height: 100%;
    align-items: center;
    justify-content: center;
  }

  img {
    width: 250px;
    height: 260px;
  }
}

.buttons-container {
  display: flex;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: transform 0.5s;
}

.slide-enter,
.slide-leave-to {
  transform: translateY(-50%) translateX(100vw);
}
</style>
