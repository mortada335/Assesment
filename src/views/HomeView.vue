<script setup lang="ts">
import { Button } from '@/components/ui/button/'
import { Input } from '@/components/ui/input'
import { ref } from 'vue'

const searchQuery = ref('')
const genderData: any = ref(null)
const isLoading = ref(false)

const fetchGen = async () => {
  if (!searchQuery.value.trim()) return

  isLoading.value = true
  genderData.value = null // Reset previous data

  try {
    const response = await fetch(`https://api.genderize.io?name=${searchQuery.value}`)

    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`)
    }

    genderData.value = await response.json()
  } catch (error) {
    console.error(error)
  } finally {
    isLoading.value = false
  }
}
</script>

<template>
  <div>
    <div class="p-6">
      <h1 class="text-4xl max-w-xs font-bold text-center md:max-w-lg mx-auto">
        Predict the gender of a person based on your name.
      </h1>
    </div>

    <div
      class="mx-auto mt-5 h-full flex max-w-xs md:max-w-lg items-center gap-2 justify-center text-center"
    >
      <Input required v-model="searchQuery" type="text" placeholder="Enter Your Name" />
      <Button @click="fetchGen()" :disabled="isLoading">
        <span
          v-if="isLoading"
          class="animate-spin border-2 border-t-transparent rounded-full w-5 h-5 border-white"
        ></span>
        <span v-else>Search</span>
      </Button>
    </div>

    <!-- Loading State -->
    <div v-if="isLoading" class="text-center mt-5">
      <div
        class="animate-spin border-4 border-t-transparent border-blue-500 rounded-full w-10 h-10 mx-auto"
      ></div>
      <p class="text-gray-500 dark:text-white mt-2">Fetching data...</p>
    </div>

    <!-- Result Display -->
    <div
      v-if="genderData"
      class="mx-auto mt-5 max-w-xs bg-red-300 p-5 rounded-md font-mono font-bold dark:bg-blue-500 md:max-w-lg"
    >
      <p class="uppercase">your name here</p>
      <p>
        Gender: <span class="text-gray-500 dark:text-red-200">{{ genderData.gender }}</span>
      </p>
      <p>
        Count: <span class="text-gray-500 dark:text-red-200">{{ genderData.count }}</span>
      </p>
    </div>

    <!-- Default Message -->
    <div
      v-else-if="!isLoading"
      class="mx-auto mt-5 max-w-xs bg-red-300 p-5 rounded-md font-mono font-bold dark:bg-blue-500 md:max-w-lg"
    >
      <p class="text-red-500 dark:text-white">There is not enough information.</p>
    </div>
  </div>
</template>
