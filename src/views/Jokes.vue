<template>
  <div class="flex flex-col items-center justify-center gap-4 p-6">
    <h1 class="text-3xl font-bold text-center">Grab ten random jokes!</h1>

    <div class="flex gap-5">
      <Select v-model="selectedCategory">
        <SelectTrigger class="dark:bg-blue-700 w-60">
          <SelectValue placeholder="Select a category" />
        </SelectTrigger>
        <SelectContent>
          <SelectGroup>
            <SelectItem v-for="category in categories" :key="category" :value="category">
              {{ category }}
            </SelectItem>
          </SelectGroup>
        </SelectContent>
      </Select>
      <Button class="dark:bg-blue-700 rounded px-2" @click="fetchJokes">GRAB</Button>
    </div>

    <!-- Jokes List -->
    <div v-if="jokes.length > 0" class="w-full max-w-lg space-y-4">
      <div
        v-for="(joke, index) in jokes"
        :key="joke.id"
        class="p-4 bg-orange-100 dark:bg-orange-900 rounded-lg shadow-md"
      >
        <p class="font-semibold">{{ joke.setup }}</p>
        <button
          @click="togglePunchline(index)"
          class="mt-2 px-3 py-2 bg-slate-200 rounded-lg dark:bg-black"
        >
          Punchline
        </button>
        <p v-if="visiblePunchline === index" class="mt-2 text-gray-700 dark:text-white">
          {{ joke.punchline }}
        </p>
      </div>
    </div>

    <!-- Error Message (Hidden Initially) -->
    <div
      v-if="showErrorMessage"
      class="w-full max-w-lg p-4 bg-red-100 text-red-600 rounded-lg shadow-md"
    >
      {{ errorMessage }}
    </div>
  </div>
</template>

<script setup lang="ts">
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'
import { ref } from 'vue'

const visiblePunchline = ref<number | null>(null)
const togglePunchline = (index: number | null) => {
  visiblePunchline.value = visiblePunchline.value === index ? null : index
}

const categories = ['General', 'Programming', 'Knock-Knock', 'Food']
const selectedCategory = ref('General')
const jokes: any = ref([])
const errorMessage = ref('')
const showErrorMessage = ref(false)

const fetchJokes = async () => {
  try {
    jokes.value = []
    showErrorMessage.value = false

    if (!selectedCategory.value) {
      return
    }

    const response = await fetch(
      `https://official-joke-api.appspot.com/jokes/${selectedCategory.value.toLowerCase()}/ten`,
    )
    if (!response.ok) throw new Error('Failed to fetch jokes')

    const data = await response.json()

    if (data.length === 0) {
      errorMessage.value = 'There are no jokes available for this category.'
      showErrorMessage.value = true
    } else {
      jokes.value = data
    }
  } catch (error) {
    errorMessage.value = 'Failed to fetch jokes. Please try again.'
    showErrorMessage.value = true
    console.error('Error fetching jokes:', error)
  }
}
</script>

<style scoped></style>
