<template>
  <div>
    <LoginModal ref="login" />

    <button class="button" @click="openModal()">
      Show Modal
    </button>
  </div>
</template>

<script>
import LoginModal from "../components/LoginModal";
export default {
  components: {
    LoginModal
  },
  layout: "empty",

  methods: {
    openModal() {
      this.$refs["login"].open();
    }
  }
};
</script>

<style lang="scss" scoped>
body {
  margin: 0px !important;
  padding: 0px !important;
}

button {
  appearance: none;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;

  display: inline-block;
  padding: 15px 25px;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
  border-radius: 8px;

  color: #fff;
  font-size: 18px;
  font-weight: 700;

  box-shadow: 3px 3px rgba(0, 0, 0, 0.4);
  transition: 0.4s ease-out;

  &:hover {
    box-shadow: 6px 6px rgba(0, 0, 0, 0.6);
  }
}
</style>
