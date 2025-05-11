<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue';
import { useRoute } from 'vue-router';

const props = defineProps({
  isDarkMode: Boolean
});

const emit = defineEmits(['toggle-dark-mode']);

const isMenuOpen = ref(false);
const isScrolled = ref(false);
const route = useRoute();

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const closeMenu = () => {
  isMenuOpen.value = false;
};

const navbarClass = computed(() => 
  isScrolled.value 
    ? 'bg-white/90 dark:bg-gray-900/90 backdrop-blur-md shadow-sm' 
    : 'bg-transparent'
);

const checkScroll = () => {
  isScrolled.value = window.scrollY > 20;
};

onMounted(() => {
  window.addEventListener('scroll', checkScroll);
  checkScroll();
});

onUnmounted(() => {
  window.removeEventListener('scroll', checkScroll);
});

const navLinks = [
  { name: 'Home', path: '/' },
  { name: 'About', path: '/about' },
  { name: 'Services', path: '/services' },
  { name: 'Projects', path: '/projects' },
  { name: 'Contact', path: '/contact' }
];

const isActive = (path) => route.path === path;
</script>

<template>
  <header 
    :class="[
      'fixed w-full top-0 z-50 transition-all duration-300', 
      navbarClass
    ]"
  >
    <div class="container-custom py-4">
      <div class="flex items-center justify-between">
        <!-- Logo -->
        <router-link to="/" class="flex items-center space-x-2" @click="closeMenu">
          <div class="flex items-center justify-center w-10 h-10 rounded-lg bg-gradient-to-r from-primary-600 to-secondary-600">
            <span class="text-white font-bold text-xl">V</span>
          </div>
          <span class="text-xl font-bold text-gray-900 dark:text-white">VisionTech</span>
        </router-link>

        <!-- Desktop Navigation -->
        <nav class="hidden md:flex items-center space-x-8">
          <ul class="flex items-center space-x-8">
            <li v-for="link in navLinks" :key="link.path">
              <router-link 
                :to="link.path" 
                :class="[
                  'nav-link',
                  isActive(link.path) ? 'text-primary-600 dark:text-primary-500' : ''
                ]"
              >
                {{ link.name }}
              </router-link>
            </li>
          </ul>
          
          <!-- Dark mode toggle -->
          <button 
            @click="emit('toggle-dark-mode')" 
            class="p-2 rounded-full hover:bg-gray-100 dark:hover:bg-gray-800 transition duration-200"
            aria-label="Toggle dark mode"
          >
            <svg v-if="props.isDarkMode" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-yellow-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
            </svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
            </svg>
          </button>
          
          <router-link to="/contact" class="btn-primary">
            Get in Touch
          </router-link>
        </nav>

        <!-- Mobile menu button -->
        <div class="flex items-center md:hidden">
          <button 
            @click="emit('toggle-dark-mode')" 
            class="p-2 mr-2 rounded-full hover:bg-gray-100 dark:hover:bg-gray-800 transition duration-200"
            aria-label="Toggle dark mode"
          >
            <svg v-if="props.isDarkMode" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-yellow-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
            </svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
            </svg>
          </button>
          
          <button 
            @click="toggleMenu" 
            class="p-2 rounded-md text-gray-600 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary-500"
            aria-label="Menu"
          >
            <svg v-if="!isMenuOpen" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Navigation -->
    <div 
      v-if="isMenuOpen" 
      class="md:hidden absolute top-full left-0 w-full bg-white dark:bg-gray-900 shadow-lg rounded-b-lg"
    >
      <div class="px-2 pt-2 pb-3 space-y-1">
        <router-link 
          v-for="link in navLinks" 
          :key="link.path" 
          :to="link.path" 
          class="block px-3 py-2 rounded-md text-base font-medium"
          :class="isActive(link.path) 
            ? 'bg-primary-50 dark:bg-gray-800 text-primary-600 dark:text-primary-500' 
            : 'hover:bg-gray-50 dark:hover:bg-gray-800 text-gray-700 dark:text-gray-300'"
          @click="closeMenu"
        >
          {{ link.name }}
        </router-link>
        
        <router-link 
          to="/contact" 
          class="block w-full text-center mt-4 btn-primary"
          @click="closeMenu"
        >
          Get in Touch
        </router-link>
      </div>
    </div>
  </header>
</template>