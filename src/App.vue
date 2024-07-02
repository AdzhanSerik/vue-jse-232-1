<script setup>
// import Counter from "./components/CounterNumber.vue";
import Sneaker from "./components/SneakersList.vue"

</script>

<template>
<div class="carts">
  <Sneaker name="Кросы" brand="Nike" price="54000" />
  <Sneaker />
  <Sneaker />
  <Sneaker />
  <Sneaker />
  <Sneaker />
  <Sneaker />
  <Sneaker />
  <Sneaker />
</div>

</template>

<style scoped>
h1 {
  font-size: 40px;
  font-weight: 300;
}
.carts {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}
</style>