<template>
  <div class="header">
    <a id="coffeeLink" name="coffees"></a>
    <header>
    <div class="logo"><img class="logo" alt="SAVA COFFEE" src="/assets/logo.png"></div>
    <div class="nav">
      <ul>
        <li><div><a href="#coffees" @click="changePage('Lots')"><img class="lotIcon" alt="Кофе" src="/assets/icons/coffeeicon.png"/></a></div></li>
        <li><div><a href="#pyros" @click="changePage('Lots')"><img class="lotIcon" alt="Сладости" src="/assets/icons/sladkicon.png"/></a></div></li>
      </ul>
    </div>
      <div class="h_icons">
        <img class="h_icon" src="/assets/icons/icon1.png" alt="Корзина"/>
        <img class="h_icon" src="/assets/icons/icon2.png" alt="Инстаграм"/>
        <img class="h_icon" src="/assets/icons/icon4.png" alt="Почта"/>
        <img class="h_icon" src="/assets/icons/icon3.png" alt="Пользователь"/>
      </div>
    <div class="enter-or-register-box">
      <template v-if="userId">
        <div class="hello">
          Добро пожаловать, {{users[userId].name}}
          <a href="#page=Logout" @click="logout">Выйти</a>
        </div>
      </template>
      <template v-else>
        <a href="#page=Enter" @click="changePage('Enter')">Войти</a>
        <a href="#page=Register" @click="changePage('Register')">Регистрация</a>
      </template>
    </div>
    </header>
  </div>
</template>

<script>
export default {
name: "Header",
  beforeCreate() {
    this.$root.$on("onEnterSuccess", () => {
      this.changePage('Lots');
    });
    this.$root.$on("onRegisterSuccess", () => {
      this.changePage('Enter');
    });
  },
  props: ["users", "userId"],
  methods: {
    changePage: function (page) {
      this.$root.$emit("onChangePage", page);
    }, logout: function() {
      this.$root.$emit("onLogout");
      this.changePage('Lots');
    }
  }
}
</script>

<style scoped>
</style>