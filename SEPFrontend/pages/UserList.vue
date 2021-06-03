<template>
  <div>
    <Navbar class="navbar" design="movielist" />
    <div class="list-container">
      <div class="search-container">
        <div class="searchbar">
          <input type="text" placeholder="Search.." name="search" id="search" />
          <button @click="searchForUser()">
            <div>
              <svg
                width="24"
                height="24"
                xmlns="http://www.w3.org/2000/svg"
                fill-rule="evenodd"
                clip-rule="evenodd"
              >
                <path
                  d="M15.853 16.56c-1.683 1.517-3.911 2.44-6.353 2.44-5.243 0-9.5-4.257-9.5-9.5s4.257-9.5 9.5-9.5 9.5 4.257 9.5 9.5c0 2.442-.923 4.67-2.44 6.353l7.44 7.44-.707.707-7.44-7.44zm-6.353-15.56c4.691 0 8.5 3.809 8.5 8.5s-3.809 8.5-8.5 8.5-8.5-3.809-8.5-8.5 3.809-8.5 8.5-8.5z"
                />
              </svg>
            </div>
          </button>
        </div>
      </div>
      <div class="no-data" v-if="!checkIfSearchExist()">
        No users have been searched in order to display
      </div>
      <div class="user-to-follow-container" v-else>
        <img src="../assets/images/No_Image_Available.jpg" alt="user profile" />
        <div class="user-to-follow-data">
          <div class="username">Username: {{ user.username }}</div>
          <div class="country">Country: {{ user.country }}</div>
          <div class="email">Email : {{ user.email }}</div>
        </div>
        <div class="button-container">
          <nuxt-link
            class="interactive-button"
            :to="`/userprofile?user=${user.username}`"
            >Profile</nuxt-link
          >
          <button class="interactive-button" @click="followUser()">
            Follow
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar";
export default {
  data() {
    return {
      user: {}
    };
  },
  layout: "empty",
  components: {
    Navbar
  },
  mounted() {
    this.getUser();
  },
  methods: {
    searchForUser() {
      var userToSearch = document.getElementById("search").value;
      var today = new Date();
      var dd = String(today.getDate()).padStart(2, "0");
      var mm = String(today.getMonth() + 1).padStart(2, "0"); //January is 0!
      var yyyy = today.getFullYear();

      today = mm + "/" + dd + "/" + yyyy;
      document.cookie = `userToSearch=${userToSearch}; expires=${today}"`;
      window.location.reload();
    },
    async getUser() {
      var userToSearch = this.getCookie("userToSearch");
      if (userToSearch.includes(";")) {
        userToSearh.split("; ").forEach(element => {
          if (element.includes("userToSearch")) {
            var split = element.split("=");
            userToSearch = split[1];
          }
        });
      }

      console.log(userToSearch);

      var token = this.getCookie("authToken").split(";")[0];

      await this.$axios
        .get(
          `https://viaucsep6group1.azurewebsites.net/User?toUser=${userToSearch}`,
          {
            headers: {
              fromToken: token
            }
          }
        )
        .then(res => {
          this.user = res.data;
        });
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
    },
    checkIfSearchExist() {
      var userToSearch = this.getCookie("userToSearch");
      if (userToSearch == null || userToSearch == "") return false;

      return true;
    },

    async followUser() {
      var token = this.getCookie("authToken");
      var userToAdd = this.getCookie("userToSearch");

      if (token.includes(";")) {
        token = token.split("; ")[0];
      }
      console.log(token);

      var res = await this.$axios.post(
        `https://viaucsep6group1.azurewebsites.net/User?userToFollow=${userToAdd}`,
        userToAdd,
        {
          headers: {
            token: token
          }
        }
      );

      console.log(res.data);

      alert(res.data);
    }
  }
};
</script>

<style lang="scss">
@import "../assets/style/butons.scss";
.search-container {
  max-height: 100%;
  min-width: 100%;

  position: absolute;
}

.searchbar {
  float: right;
  display: flex;
  box-shadow: 0 0 2px 2px #a2a2a224;
  border-radius: 12px;
  margin: 12px;
}

/* Style the search field */
.searchbar input[type="text"] {
  padding: 10px;
  font-size: 17px;
  border: none;
  width: 500px;
  background: #c5c3c3;
  border-radius: 12px;
  border-top-right-radius: 0px;
  border-bottom-right-radius: 0px;

  &:focus {
    outline: none;
  }
}

/* Style the submit button */
.searchbar button {
  width: 20%;
  padding: 10px;
  background: #2196f3;
  border-radius: 12px;
  color: white;
  font-size: 17px;
  border: none;
  border-left: none; /* Prevent double borders */
  border-top-left-radius: 0px;
  border-bottom-left-radius: 0px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.searchbar button:hover {
  transition: all 0.3s ease;
  background: #0b7dda;
}

.svg-icon {
  height: 15px;
}

.user-to-follow-container {
  display: flex;
  position: relative;
  top: 200px;
  left: 100px;
  box-shadow: 0 0 2px 2px #a2a2a224;
  padding: 10px;
  border-radius: 50px;
  width: 900px;

  img {
    border-radius: 50%;
    width: 170px;
    height: 170px;
  }

  .user-to-follow-data {
    align-self: center;
    margin-left: 22px;
    font-size: 34px;
  }
}

.button-container {
  display: flex;
  flex-flow: column;
  position: absolute;
  right: 50px;
  align-self: center;
  width: 150px;

  button {
    outline: none;
    border: none;
  }

  .interactive-button {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 10px;
    padding: 0px;
    height: 48px;
    width: 150px !important;
  }
}

.no-data {
  position: relative;
  top: 400px;
  left: 307px;
}
</style>
