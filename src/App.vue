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
  <header class="p-5 bg-white dark:bg-transparent">
    <nav class="flex justify-between items-center max-w-6xl mx-auto px-4 py-3 relative">
      <h1 class="text-blue-500 font-bold font-mono text-2xl md:text-3xl">GENDERIZE.IO</h1>

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

      <div class="flex items-center space-x-4">
        <div class="hidden md:flex">
          <DropdownMenu>
            <DropdownMenuTrigger as-child>
              <Button variant="ghost" class="relative">
                <Icon
                  icon="radix-icons:moon"
                  class="h-5 w-5 transition-transform dark:-rotate-90 dark:scale-0"
                />
                <Icon
                  icon="radix-icons:sun"
                  class="absolute h-5 w-5 rotate-90 scale-0 transition-transform dark:rotate-0 dark:scale-100"
                />
                <span class="sr-only">Toggle theme</span>
              </Button>
            </DropdownMenuTrigger>
            <DropdownMenuContent align="end">
              <DropdownMenuItem @click="colorMode = 'light'"> Light </DropdownMenuItem>
              <DropdownMenuItem @click="colorMode = 'dark'"> Dark </DropdownMenuItem>
              <DropdownMenuItem @click="colorMode = 'auto'"> System </DropdownMenuItem>
            </DropdownMenuContent>
          </DropdownMenu>
        </div>

        <div
          class="hidden md:flex items-center bg-slate-300 rounded-lg px-3 py-1 dark:text-white dark:bg-blue-600"
        >
          <span class="font-mono flex items-center">
            Ali Hasan
            <SvgIcon type="mdi" :path="path" class="ml-3" />
          </span>
        </div>

        <button @click="toggleMenu" class="md:hidden">
          <Icon icon="radix-icons:hamburger-menu" class="h-6 w-6 text-blue-500" />
        </button>
      </div>

      <div
        v-if="isMenuOpen"
        class="fixed inset-0 bg-black bg-opacity-50 z-50 flex justify-end"
        @click.self="closeMenu"
      >
        <div
          class="w-64 bg-white dark:bg-gray-900 h-full p-6 shadow-lg transform transition-transform duration-300"
        >
          <button @click="closeMenu" class="absolute top-4 right-4 text-gray-700 dark:text-white">
            <Icon icon="radix-icons:cross-1" class="h-6 w-6" />
          </button>

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

          <div class="mt-4 flex items-center bg-slate-300 rounded-lg p-3 dark:bg-blue-600">
            <SvgIcon type="mdi" :path="path" class="mr-2" />
            <span class="font-mono">Ali Hasan</span>
          </div>
        </div>
      </div>
    </nav>
  </header>

  <!-- <nav class="flex relative z-10 items-center justify-between w-full md:max-w-8xl h-fit py-7 px-2">
    <div class="flex items-center justify-center">
      <h1 class="text-teal-400 font-sans text-lg md:text-2xl uppercase font-extrabold">
        genderize.io
      </h1>
    </div>
    <div class="hidden md:flex items-center justify-center space-x-5">
      <ul class=" ">
        <li class="font-poppins text-sm text-black dark:text-white font-medium uppercase">
          <a class="text-primary" href="/">Home</a>
        </li>
      </ul>
      <ul class=" ">
        <li class="font-poppins text-sm text-black dark:text-white font-medium uppercase">
          <a class="text-teal-400" href="/jokes" aria-current="page">Jokes</a>
        </li>
      </ul>
      <ul class=" ">
        <li class="font-poppins text-sm text-black dark:text-white font-medium uppercase">
          <a class="text-primary" href="/about">About</a>
        </li>
      </ul>
    </div>
    <div class="hidden md:flex items-center justify-center space-x-4">
      <div>
        <span class="text-black dark:text-white"
          ><div class="p-2">
            <div class="flex items-center cursor-pointer">
              <svg
                stroke="currentColor"
                fill="none"
                stroke-width="2"
                viewBox="0 0 24 24"
                stroke-linecap="round"
                stroke-linejoin="round"
                class=" "
                height="25"
                width="25"
                xmlns="http://www.w3.org/2000/svg"
              >
                <circle cx="12" cy="12" r="5"></circle>
                <line x1="12" y1="1" x2="12" y2="3"></line>
                <line x1="12" y1="21" x2="12" y2="23"></line>
                <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
                <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
                <line x1="1" y1="12" x2="3" y2="12"></line>
                <line x1="21" y1="12" x2="23" y2="12"></line>
                <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
                <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
              </svg>
            </div></div
        ></span>
      </div>
      <div class="flex items-center bg-teal-100 dark:bg-teal-600 rounded-xl py-1 px-2 space-x-2">
        <span class="font-poppins text-black dark:text-white text-xs uppercase">Wisam Hasan</span
        ><span class="text-black dark:text-white"
          ><svg
            stroke="currentColor"
            fill="currentColor"
            stroke-width="0"
            viewBox="0 0 16 16"
            height="25"
            width="25"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M16 7.992C16 3.58 12.416 0 8 0S0 3.58 0 7.992c0 2.43 1.104 4.62 2.832 6.09.016.016.032.016.032.032.144.112.288.224.448.336.08.048.144.111.224.175A7.98 7.98 0 0 0 8.016 16a7.98 7.98 0 0 0 4.48-1.375c.08-.048.144-.111.224-.16.144-.111.304-.223.448-.335.016-.016.032-.016.032-.032 1.696-1.487 2.8-3.676 2.8-6.106zm-8 7.001c-1.504 0-2.88-.48-4.016-1.279.016-.128.048-.255.08-.383a4.17 4.17 0 0 1 .416-.991c.176-.304.384-.576.64-.816.24-.24.528-.463.816-.639.304-.176.624-.304.976-.4A4.15 4.15 0 0 1 8 10.342a4.185 4.185 0 0 1 2.928 1.166c.368.368.656.8.864 1.295.112.288.192.592.24.911A7.03 7.03 0 0 1 8 14.993zm-2.448-7.4a2.49 2.49 0 0 1-.208-1.024c0-.351.064-.703.208-1.023.144-.32.336-.607.576-.847.24-.24.528-.431.848-.575.32-.144.672-.208 1.024-.208.368 0 .704.064 1.024.208.32.144.608.336.848.575.24.24.432.528.576.847.144.32.208.672.208 1.023 0 .368-.064.704-.208 1.023a2.84 2.84 0 0 1-.576.848 2.84 2.84 0 0 1-.848.575 2.715 2.715 0 0 1-2.064 0 2.84 2.84 0 0 1-.848-.575 2.526 2.526 0 0 1-.56-.848zm7.424 5.306c0-.032-.016-.048-.016-.08a5.22 5.22 0 0 0-.688-1.406 4.883 4.883 0 0 0-1.088-1.135 5.207 5.207 0 0 0-1.04-.608 2.82 2.82 0 0 0 .464-.383 4.2 4.2 0 0 0 .624-.784 3.624 3.624 0 0 0 .528-1.934 3.71 3.71 0 0 0-.288-1.47 3.799 3.799 0 0 0-.816-1.199 3.845 3.845 0 0 0-1.2-.8 3.72 3.72 0 0 0-1.472-.287 3.72 3.72 0 0 0-1.472.288 3.631 3.631 0 0 0-1.2.815 3.84 3.84 0 0 0-.8 1.199 3.71 3.71 0 0 0-.288 1.47c0 .352.048.688.144 1.007.096.336.224.64.4.927.16.288.384.544.624.784.144.144.304.271.48.383a5.12 5.12 0 0 0-1.04.624c-.416.32-.784.703-1.088 1.119a4.999 4.999 0 0 0-.688 1.406c-.016.032-.016.064-.016.08C1.776 11.636.992 9.91.992 7.992.992 4.14 4.144.991 8 .991s7.008 3.149 7.008 7.001a6.96 6.96 0 0 1-2.032 4.907z"
            ></path></svg
        ></span>
      </div>
    </div>
    <div class="md:hidden flex items-center justify-end w-full">
      <span class="text-black dark:text-white"
        ><div class="p-2">
          <div class="flex items-center cursor-pointer">
            <svg
              stroke="currentColor"
              fill="none"
              stroke-width="2"
              viewBox="0 0 24 24"
              stroke-linecap="round"
              stroke-linejoin="round"
              class=" "
              height="25"
              width="25"
              xmlns="http://www.w3.org/2000/svg"
            >
              <circle cx="12" cy="12" r="5"></circle>
              <line x1="12" y1="1" x2="12" y2="3"></line>
              <line x1="12" y1="21" x2="12" y2="23"></line>
              <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
              <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
              <line x1="1" y1="12" x2="3" y2="12"></line>
              <line x1="21" y1="12" x2="23" y2="12"></line>
              <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
              <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
            </svg>
          </div></div
      ></span>
    </div>
    <div class="md:hidden flex items-center justify-end w-full cursor-pointer z-10">
      <div class="text-black dark:text-white">
        <svg
          stroke="currentColor"
          fill="currentColor"
          stroke-width="0"
          viewBox="0 0 1024 1024"
          height="30"
          width="30"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M904 160H120c-4.4 0-8 3.6-8 8v64c0 4.4 3.6 8 8 8h784c4.4 0 8-3.6 8-8v-64c0-4.4-3.6-8-8-8zm0 624H120c-4.4 0-8 3.6-8 8v64c0 4.4 3.6 8 8 8h784c4.4 0 8-3.6 8-8v-64c0-4.4-3.6-8-8-8zm0-312H120c-4.4 0-8 3.6-8 8v64c0 4.4 3.6 8 8 8h784c4.4 0 8-3.6 8-8v-64c0-4.4-3.6-8-8-8z"
          ></path>
        </svg>
      </div>
    </div>
    <div class="md:hidden"></div>
  </nav> -->

  <RouterView />
</template>
