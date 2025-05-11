<script setup>
import { ref } from 'vue';
import { useMotion } from '@vueuse/motion';

const props = defineProps({
  quote: String,
  author: String,
  role: String,
  image: String,
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
    class="card p-8 flex flex-col"
  >
    <div class="mb-4 text-primary-600 dark:text-primary-400">
      <svg class="h-8 w-8" fill="currentColor" viewBox="0 0 32 32" aria-hidden="true">
        <path d="M9.352 4C4.456 7.456 1 13.12 1 19.36c0 5.088 3.072 8.064 6.624 8.064 3.36 0 5.856-2.688 5.856-5.856 0-3.168-2.208-5.472-5.088-5.472-.576 0-1.344.096-1.536.192.48-3.264 3.552-7.104 6.624-9.024L9.352 4zm16.512 0c-4.8 3.456-8.256 9.12-8.256 15.36 0 5.088 3.072 8.064 6.624 8.064 3.264 0 5.856-2.688 5.856-5.856 0-3.168-2.304-5.472-5.184-5.472-.576 0-1.248.096-1.44.192.48-3.264 3.456-7.104 6.528-9.024L25.864 4z" />
      </svg>
    </div>
    <blockquote class="flex-1">
      <p class="text-lg font-medium text-gray-900 dark:text-white mb-7">{{ quote }}</p>
    </blockquote>
    <div class="flex items-center">
      <img :src="image" alt="testimonial author" class="h-12 w-12 rounded-full object-cover" loading="lazy" />
      <div class="ml-4">
        <div class="text-base font-medium text-gray-900 dark:text-white">{{ author }}</div>
        <div class="text-sm text-gray-500 dark:text-gray-400">{{ role }}</div>
      </div>
    </div>
  </div>
</template>