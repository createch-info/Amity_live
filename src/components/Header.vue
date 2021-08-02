<template>
  <div class="rootdiv">
    <div>
      <b-navbar toggleable="lg" type="dark">
        <b-navbar-brand :href="href">
          <b-img-lazy
            class="logo"
            src="https://amityhealthcaregroup.com/wp-content/uploads/2019/03/amity-logo-1.png"
          ></b-img-lazy>
        </b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <div v-if="isAdmin" class="resalign">
            <b-navbar-nav class="testing_main" is-nav v-if="isAdmin">
              <b-nav-item
                :active="$route.name === 'seminarCreate'"
                class="navlink"
                href="/education/#/admin/seminar/create"
              >Create Seminar</b-nav-item>
              <b-nav-item
                :active="$route.name === 'seminarRegister'"
                href="/education/#/admin/seminar/register"
                class="navlink"
              >Register</b-nav-item>
              <b-nav-item
                :active="($route.name === 'seminarscheduled') || ($route.name === 'dashbord')"
                href="/education/#/admin/seminar/scheduled"
                class="navlink"
              >Scheduled Seminars</b-nav-item>
              <b-nav-item @click.stop="logout" href="#" class="navlink">LogOut</b-nav-item>
            </b-navbar-nav>
          </div>
          <div v-else class="resalign">
            <b-navbar-nav>
              <b-nav-item
                style="width:65px;font-size:15px"
                :active="false"
                class="navlink"
                href="https://amityhealthcaregroup.com"
                >HOME
              </b-nav-item>
              <b-nav-item
                style="width:110px;font-size:15px"
                href="https://amityhealthcaregroup.com/about-us/"
                class="navlink"
                >ABOUT US
              </b-nav-item>
              <!-- <b-nav-item href="/#/" class="navlink">SERVICES</b-nav-item> -->
            </b-navbar-nav>
            <b-navbar-nav>
              <b-nav-item-dropdown
                class="service_nav"
                style="width:130px;font-size:15px"
              >
                <template slot="button-content">                  
                  SERVICES
                </template>
                <b-dropdown-item
                  href="https://amityhealthcaregroup.com/consulting-services/"
                  >Consulting Services
                </b-dropdown-item>
                <b-dropdown-item
                  href="https://amityhealthcaregroup.com/outsourcing-services/"
                  >Outsourcing Services
                </b-dropdown-item>
                <b-dropdown-item
                  href="https://amityhealthcaregroup.com/services/continued-education/"
                >
                  Ongoing Training/<br />Continued Education
                </b-dropdown-item>
                <b-dropdown-item
                  href="https://amityhealthcaregroup.com/services/cna-hha-competency/"
                >
                  CNA / HHA Competency
                </b-dropdown-item>
                <b-dropdown-item
                  href="https://amityhealthcaregroup.com/services/nursing-competencies/"
                >
                  Skilled Nursing<br />Competency
                </b-dropdown-item>
              </b-nav-item-dropdown>
            </b-navbar-nav>
            <b-navbar-nav>
              <b-nav-item
                style="width:110px;font-size:15px"
                :active="true"
                href="https://amityhealthcaregroup.com/education/#/"
                class="navlink"
                >EVENTS
              </b-nav-item>
              <b-nav-item
                style="width:110px;font-size:15px;margin-left:-27px"
                href="https://amityhealthcaregroup.com/resources/"
                class="navlink resource"
                >RESOURCES
              </b-nav-item>
              <b-nav-item
                style="width:125px;font-size:15px"
                href="https://amityhealthcaregroup.com/contact/"
                class="navlink"
                >CONTACT US
              </b-nav-item>
              
            </b-navbar-nav>
           
          </div>

        </b-collapse>
         <div class="listserv justify-content-end">
            
            <input
              id="sideinput"
              placeholder="Subscribe to Listerv"
              type="text"
              v-model="email"
             
            />
            <input
              type="button"
              id="sidebutton"
              class=" divwpcusto8 button"
              v-on:click="subscribe"
              
            />
          </div>

      </b-navbar>
      <strong v-show="error" class="mc_error_msg"
              >Email already exists in Listserv.</strong
            >
            <strong v-show="success" class="mc_success_msg"
              >Email successfully added to Listserv.</strong
            >
            <strong v-show="network" class="mc_network_msg"
              >Network Error.</strong
            >
            <strong v-show="valid" class="mc_valid_msg">Invalid Email.</strong>
            <strong v-show="blank" class="mc_blank_msg"
              >You must fill in Email Address.</strong
            >
            <strong v-show="opt" class="mc_opt_msg"
              >Please watch for an email from Amity <br />admin and opt-in to be
              added to Listserv.</strong
            >
      
      <!-- <b-navbar toggleable="lg" type="dark" variant>
		  <b-navbar-brand :href="href">
			<b-img-lazy
			  class="logo"
			  src="https://www.amityhealthcaregroup.com/wp-content/uploads/2019/03/amity-logo-1.png"
			></b-img-lazy>
		  </b-navbar-brand>

		  <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
		  <b-collapse id="nav-collapse" is-nav>
			<b-navbar-nav class="testing_main" is-nav v-if="isAdmin">
			  <b-nav-item :active="$route.name === 'seminarCreate'" class="navlink" href="/education/#/admin/seminar/create">Create Seminar</b-nav-item>
			  <b-nav-item :active="$route.name === 'seminarRegister'" href="/education/#/admin/seminar/register" class="navlink">Register</b-nav-item>
			  <b-nav-item  :active="($route.name === 'seminarscheduled') || ($route.name === 'dashbord')"
				href="/education/#/admin/seminar/scheduled"
				class="navlink"
			  >Scheduled Seminars</b-nav-item>
			  <b-nav-item @click.stop="logout" href="#" class="navlink">LogOut</b-nav-item>
			</b-navbar-nav>

			<b-navbar-nav class="testing_main" is-nav v-else>
			  <b-nav-item :active="false" class="navlink" href="https://amityhealthcaregroup.com" >HOME</b-nav-item>
			  <b-nav-item href="https://amityhealthcaregroup.com/about-us/" class="navlink">ABOUT US</b-nav-item>
			  <b-nav-item href="/#/" class="navlink">SERVICES</b-nav-item>

			  <b-nav-item :active="true" href="https://amityhealthcaregroup.com/education/#/" class="navlink">EDUCATION</b-nav-item>
			  <b-nav-item href="https://amityhealthcaregroup.com/resources/" class="navlink">RESOURCES</b-nav-item>
			  <b-nav-item href="https://amityhealthcaregroup.com/contact/" class="navlink">CONTACT US</b-nav-item>
			</b-navbar-nav>
		  </b-collapse>
		</b-navbar>-->
    </div>
    <div class="page_header">{{$route.meta.title}}</div>
  </div>
</template>

<script>
import Extra from "./../extra";
import EventBus from "./../eventBus";
import VueToast from "vue-toast-notification";
import axios from "axios";
import "vue-toast-notification/dist/theme-sugar.css";
Vue.use(VueToast);

export default {
  data() {
    email: "";

    return {
      isAdmin: Extra.isAuthenticated(),
      error: false,
      success: false,
      network: false,
      valid: false,
      blank: false,
      opt: false,
      email: ""
    };
  },
  computed: {
    href() {
      return Extra.isAuthenticated() ? "/#/admin" : "/";
    },
  },

  created() {
    this.$root.$on("ADMIN_LOGIN", this.loginAdmin);
  },

  watch: {
    $route: function(ob) {},
  },
  methods: {
    loginAdmin() {
      this.isAdmin = true;
    },
    emailChange() {
      console.log("email");
    },
    async subscribe() {
      console.log("email", this.email);
      var pattern = new RegExp(
        /^(("[\w-\s]+")|([\w-]+(?:\.[\w-]+)*)|("[\w-\s]+")([\w-]+(?:\.[\w-]+)*))(@((?:[\w-]+\.)*\w[\w-]{0,66})\.([a-z]{2,6}(?:\.[a-z]{2})?)$)|(@\[?((25[0-5]\.|2[0-4][0-9]\.|1[0-9]{2}\.|[0-9]{1,2}\.))((25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})\.){2}(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})\]?$)/i
      );
      if (this.email === "" || typeof this.email === "undefined") {
        console.log("demo");
        this.blank = true;
        this.valid = false;
        this.success = false;
        this.network = false;
        this.error = false;
        this.opt = false;
      } else if (!pattern.test(this.email)) {
        this.valid = true;
        this.success = false;
        this.network = false;
        this.error = false;
        this.blank = false;
        this.opt = false;
      } else {
        try {
          var email = this.email;
          var res = await axios.get(
            "https://amityhealthcaregroup.com/education/api/admin/addcontact/" +
              email
          );
          // var res = await axios.get(
          //   "http://localhost:8000/api/admin/addcontact/" +
          //     email
          // );
          if (res.data.code === 200) {
            this.success = true;
            this.error = false;
            this.network = false;
            this.valid = false;
            this.blank = false;
            this.opt = false;
          } else if (res.data.code === 400) {
            this.success = false;
            this.error = true;
            this.network = false;
            this.valid = false;
            this.blank = false;
            this.opt = false;
          } else {
            this.success = false;
            this.error = false;
            this.network = false;
            this.valid = false;
            this.blank = false;
            this.opt = true;
          }
        } catch (e) {
          console.log(e.message);
          if (e.message === "Request failed with status code 400") {
            this.error = true;
            this.success = false;
            this.network = false;
            this.valid = false;
            this.blank = false;
          } else {
            this.success = false;
            this.error = false;
            this.network = false;
            this.valid = false;
            this.blank = false;
            this.opt = true;
          }
        }
      }
    },
    logout() {
      Extra.logout().then((res) => {
        window.location.reload();
        this.$router.push({
          path: "/",
        });
      });
    },
  },
};
</script>

<style scoped>
.badge {
  width: 21px;
}

input#sideinput {
  float: left !important;
  width: 67% !important;
  border-radius: 50px 0 0 50px !important;
  padding: 8px !important;
  height: 44px !important;
  position: relative !important;
  right: 0 !important;
  border: 1px solid #ebebeb;
}

strong.mc_error_msg {
  font-size: 15px;
  font-weight: 100;
  background: #ff0000e0;
  padding: 5px 15px;
  top: 70px;
  position: absolute;
  color: #fff;
  right: 75px;
}
strong.mc_success_msg {
  font-size: 15px;
  font-weight: 100;
  background: #089436e0;
  padding: 5px 15px;
  top: 70px;
  position: absolute;
  color: #fff;
  right: 75px;
}
strong.mc_opt_msg {
  font-size: 15px;
  font-weight: 100;
  background: #ff0000e0;
  padding: 5px 15px;
  top: 70px;
  position: absolute;
  color: #fff;
  right: 75px;
}

strong.mc_network_msg {
  font-size: 15px;
  font-weight: 100;
  background: #ff0000e0;
  padding: 5px 15px;
  top: 70px;
  position: absolute;
  color: #fff;
  right: 75px;
}
strong.mc_valid_msg {
  font-size: 15px;
  font-weight: 100;
  background: #ff0000e0;
  padding: 5px 15px;
  top: 70px;
  position: absolute;
  color: #fff;
  right: 75px;
}

strong.mc_blank_msg {
  font-size: 15px;
  font-weight: 100;
  background: #ff0000e0;
  padding: 5px 15px;
  top: 70px;
  position: absolute;
  color: #fff;
  right: 75px;
}


@media only screen and (min-width: 300px) and (max-width: 992px) {
  strong.mc_blank_msg,
  strong.mc_network_msg,
  strong.mc_valid_msg,
  strong.mc_success_msg,
  strong.mc_error_msg {
    top: 110px;
    font-size: 11px;
    right: 150px;
  }
  input#sideinput{
    width: 160px !important;
    left: 65px;
    top: 2px;
    height: 35px !important;
  }
  #sidebutton{
    left: 65px;
    max-height: 37px;
    top: -6px;
  }
  strong.mc_opt_msg {
    top: 110px;
    font-size: 8px;
    right: 150px;
  }
  .nav-item.navlink.resource {
    margin-left: -2px !important;
  }
}

#sidebutton {
  /* font-size: 13px; */
  border: none;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  border-radius: 3px;
  letter-spacing: 0.03em;
  color: #fff;
  background-color: #aaa;
  box-sizing: border-box;
  height: 32px;
  line-height: 32px;
  padding: 0 30px;
  display: inline-block;
  margin: 0;
  transition: all 0.23s ease-in-out 0s;
  height: 43px !important;
  background-color: #2050b0 !important;
  margin-top: 7px!important;
}
input#sideinput:focus {
  border-color: black;
  outline: 0;
}
input#sidebutton:focus {
  /* border-color: black; */
  outline: 0;
}

.divwpcusto8 {
  float: left;
  width: 20%;
  display: block;
  position: relative;
  top: -7px;
  margin-top: -25px;
  color: transparent !important;
  background-image: url(https://amityhealthcaregroup.com/wp-content/themes/medici/arrow_03.png) !important;
  background-repeat: no-repeat !important;
  background-size: 20px !important;
  background-position: center !important;
  border-radius: 0 25px 25px 0;
  height: 44px;
  min-height: 20px;
  float: left !important;
  width: 5% !important;
  display: block !important;
  border-radius: 0 50px 50px 0 !important;
  margin: 0 !important;
  clear: none !important;
  background-color: #003f8c;
}

.iconNEW {
  background-position: left;
  color: transparent;
  position: relative;
  right: 25px;
  height: 17px;
  vertical-align: text-bottom;
}

.page_header {
  font-family: "Rubik", sans-serif !important;
  justify-content: center;
  align-items: center;
  display: flex;
  padding-bottom: 40px;
  padding-top: 40px;
  color: white;
  font-weight: 500;
  font-size: 40px;
  width: 100%;
  height: 50px;
  background-color: #003f8c;
  margin-bottom: 20px;
}

.submit_btn {
  width: 40px;
  background-color: #003f8c;
  border-radius: 25px;
  color: transparent;
  background-image: url("https://amityhealthcaregroup.com/wp-content/themes/medici/arrow_03.png");
  background-repeat: no-repeat;
  background-size: 20px;
  background-position: center;
  border-radius: 0 25px 25px 0;
}

.active {
  color: #003f8c !important;
  border-radius: 50px;
  border: 2px solid transparent;
}

.custom_textBox {
  max-width: 100%;
  width: 250px;
  margin-right: 0px;
  height: 36px;
  padding: 0 5px;
  border: 2px solid #003f8c;
  border-right: none;
  border-radius: 25px 0 0 25px;
}

.testing_main {
  display: flex;
  flex: 1;
  justify-content: space-around;
}

@import url("https://fonts.googleapis.com/css?family=Rubik&display=swap");
.nav_main {
  height: 90px;
  padding-left: 15px;
  padding-right: 60px;
}

.nav-item > a {
  font-weight: 800;
  font-family: "Rubik", sans-serif !important;
  /* color: #003f8c !important; */
  text-decoration-color: #003f8c !important;
  border-radius: 50px;
  border: 2px solid transparent;
  text-transform: uppercase;
  text-decoration: none;
}

.nav-item > a:hover {
  color: #003f8c !important;
  border-radius: 50px;
  border: 2px solid #003f8c;
}

.dropdown-item > a:hover {
  color: #003f8c !important;
  border-radius: 50px;
  border: 2px solid #003f8c;
}

a.nav-link.active {
  color: #003f8c !important;
  border-radius: 50px;
  border: 2px solid #003f8c;
}

.logo {
  height: 100%;
  width: 67%;
}

.nav-link {
  color: black !important;
}

.row.pageheadertext {
  background: #003f8c;
  color: #fff;
  text-align: center;
  padding: 5px;
  display: block;

  margin-bottom: 30px !important;
}

h3.pageheadertext {
  margin: 0px !important;
  padding: 5px;
  text-transform: uppercase;
}

.label01.col {
  font-weight: 800;
  color: #000;
  text-align: left;
}

button.navbar-toggler {
  background: #003f8c;
  right: 0px;
  float: right !important;
}

.navbar-expand-lg .navbar-nav {
  /* display: inline !important; */
}

nav.navbar.navbar-dark.navbar-expand-lg {
  padding: 20px;
}

@media (min-width: 769px) {
  .resalign {
    display: inherit;
  }

  a.nav-link {
    width: auto !important;
    float: left !important;
    margin: 0px 5px !important;
  }
}

@media (max-width: 768px) {
  .page_header {
    padding-bottom: 0px;
    padding-top: 0px;
    font-size: 18px;
  }

  .resalign {
    /* display: inline-flex; */
  }

  a.nav-link {
    width: 100% !important;
  }

  a.nav-link.active {
    border: none;
  }

  .navbar-dark .navbar-brand {
    width: 70% !important;
    float: left !important;
  }
}

li.nav-item.navlink.buttonspecial a {
  background: #003f8c;
  color: #fff !important;
  padding: 5px 15px;
  float: right !important;
}
.listserv {
    width: 32%!important;
    padding-right: 0px!important;
    display: flex!important;
}
@media(min-width:1200px){
  .container{
    max-width: 1530px!important;
  }
}

</style>
