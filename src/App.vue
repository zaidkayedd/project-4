<script setup>
import { ref, onMounted, watch } from 'vue'
import { useRoute } from 'vue-router'
import { usePreferredDark } from '@vueuse/core'
import Navbar from './components/layout/Navbar.vue'
import Footer from './components/layout/Footer.vue'

const isDarkMode = ref(usePreferredDark().value)
const route = useRoute()

// Initialize dark mode based on user preference or local storage
onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  if (savedTheme) {
    isDarkMode.value = savedTheme === 'dark'
  }
  applyTheme()
})

// Watch for changes in dark mode and apply theme
watch(isDarkMode, () => {
  applyTheme()
  localStorage.setItem('theme', isDarkMode.value ? 'dark' : 'light')
})

const applyTheme = () => {
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }
}

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value
}
</script>

<template>
  <div class="flex flex-col min-h-screen">
    <Navbar :isDarkMode="isDarkMode" @toggle-dark-mode="toggleDarkMode" />
    
    <main class="flex-grow">
      <router-view v-slot="{ Component }">
        <transition name="page" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>
    
    <Footer />
  </div>
</template>

<style>
.page-enter-active,
.page-leave-active {
  transition: opacity 0.3s, transform 0.3s;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>