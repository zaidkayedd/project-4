<script setup>
import { ref } from 'vue';
import { useMotion } from '@vueuse/motion';

const props = defineProps({
  title: String,
  description: String,
  icon: String,
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
    class="card p-6 hover:translate-y-[-8px]"
  >
    <div class="h-12 w-12 flex items-center justify-center rounded-md bg-primary-100 dark:bg-primary-900/30 text-primary-600 dark:text-primary-400 mb-5">
      <span v-html="icon"></span>
    </div>
    <h3 class="text-xl font-semibold text-gray-900 dark:text-white mb-3">{{ title }}</h3>
    <p class="text-gray-600 dark:text-gray-400">{{ description }}</p>
  </div>
</template>