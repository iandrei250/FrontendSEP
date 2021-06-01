<template>
  <div class="container">
    <transition name="fade" appear>
      <div class="modal-overlay" v-if="showModal" @click="close"></div>
    </transition>
    <transition name="slide" appear>
      <div class="modal" v-if="showModal">
        <div class="first-half">
          <h1>Create An Account</h1>
          <div class="login-form">
            <div class="name">
              <input
                type="text"
                id="first-name"
                name="First Name"
                placeholder="First Name"
                ref="First Name"
              />
              <input
                type="text"
                id="last-name"
                name="Last Name"
                placeholder="Last Name"
                ref="Last Name"
              />
            </div>
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
            <input
              type="email"
              id="email"
              name="email"
              placeholder="Email"
              ref="email"
            />

            <input class="birthday" type="date" id="birthday" name="birthday" />
            <div class="country-dropdown">
              <vue-select
                id="country"
                :options="items"
                class="dropdown"
                placeholder="Country"
                :reduce="country => (selectedCountry = country)"
              >
              </vue-select>
            </div>

            <div class="buttons-container">
              <button class="button" @click="register">
                Register
              </button>
              <button class="button" @click="close">
                Cancel
              </button>
            </div>
          </div>
        </div>
        <div class="second-half">
          <div class="login-icon">
            <img
              src="../assets/images/Forms/RegisterIcon.png"
              alt="Register Icon"
            />
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import vueSelect from "vue-select";
import "vue-select/dist/vue-select.css";
export default {
  components: {
    vueSelect
  },

  data() {
    return {
      selectedCountry: "",
      showModal: false,
      items: [
        "Afghanistan",
        "Albania",
        "Algeria",
        "Andorra",
        "Angola",
        "Anguilla",
        "Antigua &amp; Barbuda",
        "Argentina",
        "Armenia",
        "Aruba",
        "Australia",
        "Austria",
        "Azerbaijan",
        "Bahamas",
        "Bahrain",
        "Bangladesh",
        "Barbados",
        "Belarus",
        "Belgium",
        "Belize",
        "Benin",
        "Bermuda",
        "Bhutan",
        "Bolivia",
        "Bosnia &amp; Herzegovina",
        "Botswana",
        "Brazil",
        "British Virgin Islands",
        "Brunei",
        "Bulgaria",
        "Burkina Faso",
        "Burundi",
        "Cambodia",
        "Cameroon",
        "Cape Verde",
        "Cayman Islands",
        "Chad",
        "Chile",
        "China",
        "Colombia",
        "Congo",
        "Cook Islands",
        "Costa Rica",
        "Cote D Ivoire",
        "Croatia",
        "Cruise Ship",
        "Cuba",
        "Cyprus",
        "Czech Republic",
        "Denmark",
        "Djibouti",
        "Dominica",
        "Dominican Republic",
        "Ecuador",
        "Egypt",
        "El Salvador",
        "Equatorial Guinea",
        "Estonia",
        "Ethiopia",
        "Falkland Islands",
        "Faroe Islands",
        "Fiji",
        "Finland",
        "France",
        "French Polynesia",
        "French West Indies",
        "Gabon",
        "Gambia",
        "Georgia",
        "Germany",
        "Ghana",
        "Gibraltar",
        "Greece",
        "Greenland",
        "Grenada",
        "Guam",
        "Guatemala",
        "Guernsey",
        "Guinea",
        "Guinea Bissau",
        "Guyana",
        "Haiti",
        "Honduras",
        "Hong Kong",
        "Hungary",
        "Iceland",
        "India",
        "Indonesia",
        "Iran",
        "Iraq",
        "Ireland",
        "Isle of Man",
        "Israel",
        "Italy",
        "Jamaica",
        "Japan",
        "Jersey",
        "Jordan",
        "Kazakhstan",
        "Kenya",
        "Kuwait",
        "Kyrgyz Republic",
        "Laos",
        "Latvia",
        "Lebanon",
        "Lesotho",
        "Liberia",
        "Libya",
        "Liechtenstein",
        "Lithuania",
        "Luxembourg",
        "Macau",
        "Macedonia",
        "Madagascar",
        "Malawi",
        "Malaysia",
        "Maldives",
        "Mali",
        "Malta",
        "Mauritania",
        "Mauritius",
        "Mexico",
        "Moldova",
        "Monaco",
        "Mongolia",
        "Montenegro",
        "Montserrat",
        "Morocco",
        "Mozambique",
        "Namibia",
        "Nepal",
        "Netherlands",
        "Netherlands Antilles",
        "New Caledonia",
        "New Zealand",
        "Nicaragua",
        "Niger",
        "Nigeria",
        "Norway",
        "Oman",
        "Pakistan",
        "Palestine",
        "Panama",
        "Papua New Guinea",
        "Paraguay",
        "Peru",
        "Philippines",
        "Poland",
        "Portugal",
        "Puerto Rico",
        "Qatar",
        "Reunion",
        "Romania",
        "Russia",
        "Rwanda",
        "Saint Pierre &amp; Miquelon",
        "Samoa",
        "San Marino",
        "Satellite",
        "Saudi Arabia",
        "Senegal",
        "Serbia",
        "Seychelles",
        "Sierra Leone",
        "Singapore",
        "Slovakia",
        "Slovenia",
        "South Africa",
        "South Korea",
        "Spain",
        "Sri Lanka",
        "St Kitts &amp; Nevis",
        "St Lucia",
        "St Vincent",
        "St. Lucia",
        "Sudan",
        "Suriname",
        "Swaziland",
        "Sweden",
        "Switzerland",
        "Syria",
        "Taiwan",
        "Tajikistan",
        "Tanzania",
        "Thailand",
        "Timor L'Este",
        "Togo",
        "Tonga",
        "Trinidad &amp; Tobago",
        "Tunisia",
        "Turkey",
        "Turkmenistan",
        "Turks &amp; Caicos",
        "Uganda",
        "Ukraine",
        "United Arab Emirates",
        "United Kingdom",
        "Uruguay",
        "Uzbekistan",
        "Venezuela",
        "Vietnam",
        "Virgin Islands (US)",
        "Yemen",
        "Zambia",
        "Zimbabwe"
      ]
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

    async register() {
      var firstName = document.getElementById("first-name").value;
      var lastName = document.getElementById("last-name").value;
      var username = document.getElementById("username").value;
      var pass = document.getElementById("password").value;
      var email = document.getElementById("email").value;
      var birthday = document.getElementById("birthday").value;
      var birthdayDate = new Date(birthday);
      var country = this.selectedCountry;

      var user = {
        name: firstName + " " + lastName,
        username: username,
        password: pass,
        email: email,
        birthday: birthday,
        country: country
      };

      let res = await this.$axios.post(
        "https://viaucsep6group1.azurewebsites.net/Auth/Register",
        user
      );
      console.log(res.data);
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
  z-index: 98;
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

  width: 795px;
  height: 553px;
  background-color: #fff;
  border-radius: 16px;

  padding: 25px;

  h1 {
    color: #222;
    font-size: 32px;
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

  .birthday {
    text-transform: uppercase;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    color: #686767;
    font-weight: 500;
  }
}

.first-half {
  height: 100%;
  width: 50%;
  align-self: center;

  .name {
    display: flex;
    #first-name {
      width: 50%;
    }

    #last-name {
      width: 50%;
    }
  }
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
    width: 370px;
    height: 360px;
  }
}

.country-dropdown {
  margin: 8px;
  height: 32px;
  border-radius: 11px;
  border: 2px solid #3e3e3e;
  text-align: left;
  z-index: 99;
  outline: none;
  cursor: pointer;
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
