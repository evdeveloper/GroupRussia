<script setup lang="ts">

import { ref, onBeforeMount } from 'vue'
import Card from '@/components/Card.vue'

interface IPokemons {
  id: number
  name: string
  url: string
  image: string
  experience: number
  types: string
}

const isLoading = ref<boolean>(true)
const errorClass = ref<boolean>(false)
let msg = ref<string>('Загрузка...')
let pokemons = ref<IPokemons[]>([])

onBeforeMount(async () => {
  try {
    isLoading.value = false
    const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=50')
    const data = await response.json()
    data.results.forEach(async (pokemon: any) => {
      const response = await fetch(`${pokemon.url}`)
      const data = await response.json()
      console.log(data)
      pokemons.value.push(data)
      return pokemons
    })
  } catch (error) {
    isLoading.value = true
    errorClass.value = true
    msg.value = 'Произошла ошибка получения данных...'
  }
})

</script>

<template>
  <div v-if="isLoading" :class="[errorClass ? 'text-red-500 loader' : 'loader']">{{ msg }}</div>
  <div v-else class="container">
    <h1 class="text-3xl text-center py-6 mb-5 text-white">Список покемонов</h1>
    <div class="grid grid-cols-4 gap-6">
      <template v-for="pokemon in pokemons" :key="pokemon.id">
        <Card :pokemon="pokemon" />
      </template>
    </div>
  </div>
  
</template>

<style lang="scss" scoped>
  
</style>
