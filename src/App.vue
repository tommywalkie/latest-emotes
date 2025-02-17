<template>
  <div class="min-h-screen flex flex-col bg-gray-100 dark:bg-secondary relative">
    <div class="absolute top-3 right-3">
      <DarkModeToggle />
    </div>

    <!-- Minified logo + site name -->
    <MinifiedHeader :show="showMinifiedHeader" />

    <!-- Main content wrapper -->
    <div class="flex-grow">
      <div class="">
        <!-- Header Observer Target -->
        <div ref="headerObserverTarget" class="absolute top-0 h-32"></div>

        <div class="flex flex-col items-center text-center max-w-7xl mx-auto p-0 sm:p-8 pt-5 sm:pt-8 md:pt-10 lg:pt-12">
          <a href="/">
            <img src="/logo.svg" alt="7TV Lite" class="w-24 h-24 mb-5" />
          </a>
          <h1 class="text-2xl font-bold text-center">7TV Lite</h1>
          <p class="text-center text-gray-500 dark:text-gray-400">
            Lightweight client for browsing the latest
            <a href="https://7tv.app/" target="_blank" rel="noopener noreferrer">7TV</a>
            emotes.
          </p>
        </div>
        <div class="h-full">
          <RouterView :showMinifiedHeader="showMinifiedHeader" />
        </div>
      </div>
    </div>

    <!-- Footer -->
    <footer class="w-full py-4 mt-auto bg-gray-200 dark:bg-secondary-400 text-gray-800 dark:text-gray-200">
      <div class="max-w-7xl mx-auto px-4">
        <div class="flex flex-col sm:flex-row items-center gap-4 sm:gap-2 justify-center">
          <p>
            <a href="https://github.com/tommywalkie/7tv-lite" target="_blank" rel="noopener noreferrer">
              <svg
                viewBox="0 0 1024 1024"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
                class="w-5 h-5 inline-block mr-1 align-sub text-nowrap fill-gray-800 dark:fill-white"
              >
                <path
                  fill-rule="evenodd"
                  clip-rule="evenodd"
                  d="M8 0C3.58 0 0 3.58 0 8C0 11.54 2.29 14.53 5.47 15.59C5.87 15.66 6.02 15.42 6.02 15.21C6.02 15.02 6.01 14.39 6.01 13.72C4 14.09 3.48 13.23 3.32 12.78C3.23 12.55 2.84 11.84 2.5 11.65C2.22 11.5 1.82 11.13 2.49 11.12C3.12 11.11 3.57 11.7 3.72 11.94C4.44 13.15 5.59 12.81 6.05 12.6C6.12 12.08 6.33 11.73 6.56 11.53C4.78 11.33 2.92 10.64 2.92 7.58C2.92 6.71 3.23 5.99 3.74 5.43C3.66 5.23 3.38 4.41 3.82 3.31C3.82 3.31 4.49 3.1 6.02 4.13C6.66 3.95 7.34 3.86 8.02 3.86C8.7 3.86 9.38 3.95 10.02 4.13C11.55 3.09 12.22 3.31 12.22 3.31C12.66 4.41 12.38 5.23 12.3 5.43C12.81 5.99 13.12 6.7 13.12 7.58C13.12 10.65 11.25 11.33 9.47 11.53C9.76 11.78 10.01 12.26 10.01 13.01C10.01 14.08 10 14.94 10 15.21C10 15.42 10.15 15.67 10.55 15.59C13.71 14.53 16 11.53 16 8C16 3.58 12.42 0 8 0Z"
                  transform="scale(64)"
                />
              </svg>
              &nbsp;Source
            </a>
          </p>
          <span class="text-gray-400 hidden sm:block">✦</span>
          <p class="text-center text-gray-500 dark:text-gray-200">
            Made with ❤️ by
            <a href="https://github.com/tommywalkie" target="_blank" rel="noopener noreferrer">tommywalkie</a>
          </p>
          <span class="text-gray-400 hidden sm:block">✦</span>
          <p>
            <router-link to="/privacy">Privacy Policy</router-link>
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import DarkModeToggle from './components/DarkModeToggle.vue'
import MinifiedHeader from './components/MinifiedHeader.vue'

const headerObserverTarget = ref<HTMLElement | null>(null)
const showMinifiedHeader = ref(false)

let observer: IntersectionObserver | null = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      showMinifiedHeader.value = !entries[0].isIntersecting
    },
    { threshold: 0 },
  )

  if (headerObserverTarget.value) {
    observer.observe(headerObserverTarget.value)
  }
})

onUnmounted(() => {
  if (observer) {
    observer.disconnect()
  }
})
</script>

<style scoped>
/* Add any additional styles here if needed */
</style>
