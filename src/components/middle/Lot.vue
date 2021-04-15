<template>
  <tr class="lot">
    <div class="lot_img">
      <img class="lot" :src="ilot.src">
    </div>
    <div class="info">
      <p>{{ ilot.name}}</p>
      <p>{{ ilot.count }}</p>
      <p>{{ ilot.cost }} руб.</p>
    </div>
  </tr>
</template>

<script>
export default {
  name: "lot",
  props: ["ilot"]
}
</script>

<style scoped>

</style>