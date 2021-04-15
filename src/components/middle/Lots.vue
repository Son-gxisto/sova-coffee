<template>
  <div class="lots">
    <div class="col"><a name="pyros"></a>
      <div class="c_title"><div class="title">Кофе</div></div>
      <div class="col_body"><Lot v-for="lot in coffee_src" :key="lot.id" :ilot="lot"></Lot></div>

    </div>
    <div class="col"><a name="pyros"></a>
      <div class="c_title"><div class="title">Пирожные</div></div>
      <div class="col_body"><Lot v-for="lot in pyro_src" :key="lot.id" :ilot="lot"></Lot></div>
    </div>
    <a name="pyros"></a>
  </div>
</template>

<script>
import Lot from "@/components/middle/Lot";
export default {
  name: "lots",
  components: {Lot},
  props: ["coffee_src", "pyro_src"]
}
</script>

<style scoped>

</style>