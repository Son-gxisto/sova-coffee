<template>
  <body>
    <Lots v-if="page === 'Lots'" :pyro_src="pyro_src" :coffee_src="coffee_src"></Lots>
    <Register v-if="page === 'Register'"></Register>
    <Enter v-if="page === 'Enter'"></Enter>
  </body>
</template>

<script>

import Lots from './middle/Lots.vue'
import Register from './middle/Register.vue'
import Enter from './middle/Enter.vue'
//<lot imgsrc="/assets/coffee/espresso.png" name="Эспрессо"></lot>
export default {
  name: "Middle.vue",
  props: ["coffee_src", "pyro_src"],
  components: {
    Lots,
    Register,
    Enter
  },
  data: function () {
    return {
      page: "Lots",
      id: null
    }
  },
  beforeCreate() {
    this.$root.$on("onChangePage", (page, id) => {
      this.page = page;
      this.id = id;
    });
  }
}
</script>

<style scoped>

</style>