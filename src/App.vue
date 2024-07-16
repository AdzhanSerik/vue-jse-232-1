<script setup>
import Header from './components/HeaderComponent.vue'
import Cards from './components/CardsItems.vue'
import { onMounted, reactive, ref, watch, provide } from 'vue'
import axios from 'axios'
import Drawer from './components/DrawerComponent.vue'

const items = ref([])
const openCart = ref(false)
const filters = reactive({
  sortBy: 'title',
  searchBy: ''
})

const openDrawer = () => {
  openCart.value = true
}
const closeDrawer = () => {
  openCart.value = false
}

provide('closeDrawer', closeDrawer)

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }
    if (filters.searchBy) {
      params.title = filters.searchBy
    }
    const { data } = await axios.get(`https://269b3b45e08bcd1a.mokky.dev/items`, {
      params
    })

    items.value = data.map((obj) => ({
      ...obj,
      isAdded: false,
      isFavourite: false
    }))
  } catch (error) {
    console.log(error)
  }
}

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeInput = (event) => {
  filters.searchBy = `*${event.target.value}*`
}

onMounted(fetchItems)
watch(filters, fetchItems)
</script>

<template>
  <Drawer v-if="openCart" />
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14 pb-2">
    <Header :openDrawer="openDrawer" />
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
            @input="onChangeInput"
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
