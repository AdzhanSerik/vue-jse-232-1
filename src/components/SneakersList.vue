<template>
  <div>
    <h1>{{ brand }}</h1>
    <h2>{{ name }}</h2>
    <span>{{ price }}</span>
  </div>
</template>

<script setup>
defineProps({
  name: String,
  brand: String,
  price: Number
})
</script>

<style scoped>
div {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 20px;
  background-color: blue;
  width: 200px;
  border-radius: 20px;
}
</style>