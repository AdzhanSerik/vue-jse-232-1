<script setup>
import Card from './CardItem.vue'

const onClickAdd = () => {
  alert('Добавлено')
}
</script>

<template>
  <div class="p-10 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-2 lg:grid-cols-4 gap-5">
    <Card
      image="/sneakers/sneakers-1.jpg"
      name="Мужские Кроссовки Nike Blazer Mid Suede"
      :price="12999"
      :isAdded="false"
      :isFavourite="true"
      :onClickAdd="onClickAdd"
    />
    <Card />
    <Card />
    <Card />
    <Card />
    <Card />
  </div>
</template>