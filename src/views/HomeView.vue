<script setup lang="ts">
import { Button } from '@/components/ui/button/'
import { Input } from '@/components/ui/input'
import { ref } from 'vue'

// const fetchJokes = async () => {
//   const response = await fetch('https://official-joke-api.appspot.com/random_joke')
//   const data = response.json()
//   console.log(data)
// }
// fetchJokes()
const searchQuery = ref('')
const genderData: any = ref(null)
const fetchGen = async () => {
  const response = await fetch(`https://api.genderize.io?name=${searchQuery.value}`)

  if (!searchQuery.value || searchQuery.value == ' ') {
    throw new Error(`HTTP error! Status: ${response.status}`)
  }

  genderData.value = await response.json()
}
</script>

<template>
  <div>
    <div class="mt-20">
      <h1 class="text-4xl font-bold text-center max-w-lg mx-auto">
        Predict the gender of a person based on your name.
      </h1>
    </div>

    <div class="mx-auto mt-5 h-full flex max-w-md items-center gap-2 justify-center text-center">
      <Input required v-model="searchQuery" id="email" type="text" placeholder="Search..." />
      <Button @click="fetchGen()" type="submit"> Search </Button>
    </div>
    <div
      v-if="genderData"
      class="mx-auto mt-5 max-w-md bg-red-300 p-5 rounded-md font-mono font-bold dark:bg-blue-500"
    >
      <p class="uppercase">your name here</p>
      <p>
        Gender: <span class="text-gray-500 dark:text-red-200">{{ genderData.gender }}</span>
      </p>
      <p>
        Count: <span class="text-gray-500 dark:text-red-200">{{ genderData.count }}</span>
      </p>
    </div>
    <div
      v-else
      class="mx-auto mt-5 max-w-md bg-red-300 p-5 rounded-md font-mono font-bold dark:bg-blue-500"
    >
      <p class="text-red-500 dark:text-white">There is no enough information.</p>
    </div>
  </div>
</template>
