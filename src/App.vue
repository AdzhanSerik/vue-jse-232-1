<script setup>
import Header from './components/HeaderComponent.vue'
import Cards from './components/CardsItems.vue'
import { onMounted, ref, watch } from 'vue'
import axios from 'axios'
// import Drawer from './components/DrawerComponent.vue'

const items = ref([])
const sortBy = ref('')

const onChangeSelect = (event) => {
  sortBy.value = event.target.value
}

onMounted(async () => {
  try {
    const { data } = await axios.get('https://269b3b45e08bcd1a.mokky.dev/items')
    items.value = data
  } catch (error) {
    console.log(error)
  }
})

watch(sortBy, async () => {
  try {
    const { data } = await axios.get(
      'https://269b3b45e08bcd1a.mokky.dev/items?sortBy=' + sortBy.value
    )
    items.value = data
  } catch (error) {
    console.log(error)
  }
})
</script>

<template>
  <!-- <Drawer /> -->
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14 pb-2">
    <Header />
    <div class="flex justify-between pr-10">
      <h2 class="font-bold text-xl p-10">Все кроссовки</h2>
      <div class="flex gap-3 items-center">
        <select
          @change="onChangeSelect"
          class="border border-gray-200 rounded-md outline-none py-2 px-2"
        >
          <option value="title">По названию</option>
          <option value="price">По возрастанию цены</option>
          <option value="-price">По убыванию цены</option>
        </select>
        <div class="relative">
          <input
            type="text"
            class="border border-gray-200 rounded-md py-2 pl-10 pr-4 focus:outline-none focus:border-gray-400"
            placeholder="Поиск..."
          />
          <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
            <img src="/search.svg" />
          </div>
        </div>
      </div>
    </div>

    <Cards :items="items" />
  </div>
</template>

<style scoped>
</style>
