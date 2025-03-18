<script setup lang="ts">
import { Button } from '@/components/ui/button'
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuTrigger,
} from '@/components/ui/dropdown-menu'
import { Icon } from '@iconify/vue'
import { useColorMode } from '@vueuse/core'
import SvgIcon from '@jamescoyle/vue-icon'
import { mdiAccount } from '@mdi/js'
import { ref } from 'vue'

const path = mdiAccount
const colorMode = useColorMode()

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}
</script>

<template>
  <header class="p-5 bg-white dark:bg-gray-900 shadow-md">
    <nav class="flex justify-between items-center max-w-6xl mx-auto px-4 py-3 relative">
      <!-- Logo -->
      <h1 class="text-blue-500 font-bold font-mono text-2xl md:text-3xl">GENDERIZE.IO</h1>

      <!-- Desktop Navigation -->
      <div class="hidden md:flex items-center space-x-7 gap-3">
        <router-link
          to="/"
          class="font-mono hover:text-blue-500"
          active-class="text-blue-500 font-bold"
          >Home</router-link
        >
        <router-link
          to="/jokes"
          class="font-mono hover:text-blue-500"
          active-class="text-blue-500 font-bold"
          >Jokes</router-link
        >
        <router-link
          to="/about"
          class="font-mono hover:text-blue-500"
          active-class="text-blue-500 font-bold"
          >About</router-link
        >
      </div>

      <!-- Right Section -->
      <div class="flex items-center space-x-4">
        <div
          class="hidden md:flex items-center bg-slate-300 rounded-lg px-3 py-1 dark:text-white dark:bg-blue-600"
        >
          <span class="font-mono flex items-center">
            Ali Hasan
            <SvgIcon type="mdi" :path="path" class="ml-3" />
          </span>
        </div>

        <!-- Mobile Menu Button -->
        <button @click="toggleMenu" class="md:hidden">
          <Icon icon="radix-icons:hamburger-menu" class="h-6 w-6 text-blue-500" />
        </button>
      </div>

      <!-- Mobile Menu -->
      <div
        v-if="isMenuOpen"
        class="fixed inset-0 bg-black bg-opacity-50 z-50 flex justify-end"
        @click.self="closeMenu"
      >
        <div
          class="w-64 bg-white dark:bg-gray-900 h-full p-6 shadow-lg transform transition-transform duration-300"
        >
          <!-- Close Button -->
          <button @click="closeMenu" class="absolute top-4 right-4 text-gray-700 dark:text-white">
            <Icon icon="radix-icons:cross-1" class="h-6 w-6" />
          </button>

          <!-- Navigation Links -->
          <div class="mt-8 flex flex-col space-y-4">
            <router-link to="/" class="text-blue-500 font-bold" @click="closeMenu"
              >Home</router-link
            >
            <router-link to="/jokes" class="text-blue-500 font-bold" @click="closeMenu"
              >Jokes</router-link
            >
            <router-link to="/about" class="text-blue-500 font-bold" @click="closeMenu"
              >About</router-link
            >
          </div>

          <!-- Dark Mode & User -->
          <div class="mt-6">
            <DropdownMenu>
              <DropdownMenuTrigger as-child>
                <Button variant="ghost" class="flex items-center">
                  <Icon icon="radix-icons:moon" class="h-5 w-5 dark:scale-100" />
                  <span class="ml-2">Theme</span>
                </Button>
              </DropdownMenuTrigger>
              <DropdownMenuContent align="end">
                <DropdownMenuItem @click="colorMode = 'light'"> Light </DropdownMenuItem>
                <DropdownMenuItem @click="colorMode = 'dark'"> Dark </DropdownMenuItem>
                <DropdownMenuItem @click="colorMode = 'auto'"> System </DropdownMenuItem>
              </DropdownMenuContent>
            </DropdownMenu>
          </div>

          <!-- User Info -->
          <div class="mt-4 flex items-center bg-slate-300 rounded-lg p-3 dark:bg-blue-600">
            <SvgIcon type="mdi" :path="path" class="mr-2" />
            <span class="font-mono">Ali Hasan</span>
          </div>
        </div>
      </div>
    </nav>
  </header>

  <RouterView />
</template>
