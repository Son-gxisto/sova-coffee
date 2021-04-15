<template>
  <div id="app">
    <Header :users="users" :userId="userId"></Header>
    <Middle :coffee_src="coffee_src" :pyro_src="pyro_src"></Middle>
    <Footer></Footer>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Header from './components/Header.vue'
import Middle from './components/Middle.vue'
import Footer from "@/components/Footer";
export default {
  //<HelloWorld msg="Welcome to Your Vue.js App"/>
  name: 'App',
  components: {
    Footer,
    Header,
    Middle
  },
  data: function () {
    return this.$root.$data;
  },
  beforeCreate() {
    this.$root.$on("onLogout", () => {
      this.userId = null;
    });
    this.$root.$on("onEnter", (login) => {
      let tusers = Object.values(this.users).filter(u => u.login === login);
      if (tusers.length) {
        this.userId = tusers[0].id;
        this.$root.$emit("onEnterSuccess");
      } else {
        this.$root.$emit("onEnterValidationError", "Invalid login/password.");
      }
    });
    this.$root.$on("onRegister", (login, name) => {
      if (!login || login.length < 3 || login.length > 16) {
        this.$root.$emit("onRegisterValidationError", "login length must be between 3 and 16");
      } else if (!(login.match("[a-z]+").toString() === login)) {
        this.$root.$emit("onRegisterValidationError", "login must contain only lowercase latin letters")
      } else if (Object.values(this.users).filter(u => u.login === login).length) {
        this.$root.$emit("onRegisterValidationError", "this login is already in use");
      } else if (!name || !name.length || name.length > 32) {
        this.$root.$emit("onRegisterValidationError", "name length must be between 1 and 32");
      } else {
        let id = Math.max(Object.keys(this.users)) + 1;
        this.$set(this.users, id, {
          id,
          login,
          name
        });
        this.$root.$emit("onRegisterSuccess");
      }
    });
  }
}
</script>

<style>
#app {
  font-family: Oswald;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
