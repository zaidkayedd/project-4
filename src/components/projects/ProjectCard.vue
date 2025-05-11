<script setup>
import { ref } from 'vue';
import { useMotion } from '@vueuse/motion';

const props = defineProps({
  title: String,
  description: String,
  image: String,
  category: String,
  link: String,
  delay: {
    type: Number,
    default: 0
  }
});

const cardRef = ref(null);

const cardMotion = useMotion(cardRef, {
  initial: {
    opacity: 0,
    y: 40,
  },
  enter: {
    opacity: 1,
    y: 0,
    transition: {
      delay: props.delay,
      duration: 700,
    }
  }
});
</script>

<template>
  <div 
    ref="cardRef"
    class="card group"
  >
    <div class="relative overflow-hidden h-60">
      <img 
        :src="image" 
        :alt="title" 
        class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
      />
      <div class="absolute inset-0 bg-gradient-to-t from-gray-900/80 to-gray-900/0"></div>
      <div class="absolute bottom-4 left-4 right-4">
        <span class="px-2 py-1 text-xs font-medium bg-primary-500 text-white rounded-md mb-2 inline-block">
          {{ category }}
        </span>
        <h3 class="text-xl font-semibold text-white">{{ title }}</h3>
      </div>
    </div>
    <div class="p-6">
      <p class="text-gray-600 dark:text-gray-400 mb-4">{{ description }}</p>
      <router-link :to="link" class="text-primary-600 dark:text-primary-500 font-medium inline-flex items-center">
        View Project
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
        </svg>
      </router-link>
    </div>
  </div>
</template>