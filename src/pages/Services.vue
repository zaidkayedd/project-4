<script setup>
import { ref, computed } from 'vue';
import { useMotion } from '@vueuse/motion';

const headerRef = ref(null);
const selectedTab = ref('web-development');

const services = [
  {
    id: 'web-development',
    title: 'Web Development',
    description: 'We create custom web applications that are fast, secure, and scalable. Our development approach focuses on performance, user experience, and maintainability.',
    features: [
      'Custom website development',
      'Progressive web applications (PWAs)',
      'E-commerce solutions',
      'Content management systems',
      'API development and integration',
      'Performance optimization'
    ],
    image: 'https://images.pexels.com/photos/3861969/pexels-photo-3861969.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" /></svg>`
  },
  {
    id: 'ui-ux-design',
    title: 'UI/UX Design',
    description: 'Our design team creates beautiful, intuitive interfaces that engage users and elevate your brand. We focus on creating experiences that are both visually stunning and highly functional.',
    features: [
      'User research and persona development',
      'Information architecture',
      'Wireframing and prototyping',
      'Visual design and branding',
      'Interaction design',
      'Usability testing'
    ],
    image: 'https://images.pexels.com/photos/196644/pexels-photo-196644.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zm0 0h12a2 2 0 002-2v-4a2 2 0 00-2-2h-2.343M11 7.343l1.657-1.657a2 2 0 012.828 0l2.829 2.829a2 2 0 010 2.828l-8.486 8.485M7 17h.01" /></svg>`
  },
  {
    id: 'mobile-development',
    title: 'Mobile Development',
    description: 'We develop native and cross-platform mobile applications that provide seamless experiences across iOS and Android devices. Our mobile solutions are built with performance and user experience in mind.',
    features: [
      'Native iOS and Android development',
      'Cross-platform solutions',
      'Mobile app UI/UX design',
      'App performance optimization',
      'Backend integration',
      'App store submission and optimization'
    ],
    image: 'https://images.pexels.com/photos/3912990/pexels-photo-3912990.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" /></svg>`
  },
  {
    id: 'digital-marketing',
    title: 'Digital Marketing',
    description: 'Our strategic marketing services help you reach your target audience and drive meaningful conversions. We develop data-driven campaigns that deliver measurable results.',
    features: [
      'Search engine optimization (SEO)',
      'Pay-per-click (PPC) advertising',
      'Social media marketing',
      'Content marketing',
      'Email marketing',
      'Analytics and reporting'
    ],
    image: 'https://images.pexels.com/photos/3182812/pexels-photo-3182812.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 3.055A9.001 9.001 0 1020.945 13H11V3.055z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.488 9H15V3.512A9.025 9.025 0 0120.488 9z" /></svg>`
  }
];

const currentService = computed(() => {
  return services.find(service => service.id === selectedTab.value);
});

const selectTab = (tabId) => {
  selectedTab.value = tabId;
};

const headerMotion = useMotion(headerRef, {
  initial: {
    opacity: 0,
    y: 40,
  },
  enter: {
    opacity: 1,
    y: 0,
    transition: {
      duration: 700,
    }
  }
});
</script>

<template>
  <div>
    <!-- Hero Section -->
    <section class="relative pt-24 pb-16 overflow-hidden bg-white dark:bg-gray-900">
      <div class="container-custom py-16">
        <div ref="headerRef" class="max-w-3xl mx-auto text-center">
          <h1 class="text-4xl md:text-5xl font-bold tracking-tight text-gray-900 dark:text-white mb-6">
            Our Services
          </h1>
          <p class="text-lg text-gray-600 dark:text-gray-300 mb-6">
            We offer a comprehensive range of digital services to help businesses thrive in the digital world.
            Our expertise spans web development, design, mobile applications, and digital marketing.
          </p>
        </div>
      </div>
    </section>

    <!-- Services Tabs Section -->
    <section class="py-24 bg-gray-50 dark:bg-gray-950">
      <div class="container-custom">
        <!-- Tabs Navigation -->
        <div 
          class="flex flex-wrap justify-center mb-12 gap-3"
          v-motion
          :initial="{ opacity: 0, y: 20 }"
          :enter="{ opacity: 1, y: 0 }"
        >
          <button 
            v-for="service in services" 
            :key="service.id"
            @click="selectTab(service.id)"
            class="px-4 py-2 rounded-md transition-colors duration-200 flex items-center"
            :class="selectedTab === service.id 
              ? 'bg-primary-600 text-white' 
              : 'bg-white dark:bg-gray-800 text-gray-600 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700'"
          >
            <span v-html="service.icon" class="mr-2"></span>
            {{ service.title }}
          </button>
        </div>
        
        <!-- Service Content -->
        <div 
          v-if="currentService"
          class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center"
        >
          <div
            v-motion
            :initial="{ opacity: 0, x: -40 }"
            :enter="{ opacity: 1, x: 0 }"
            :key="currentService.id + '-content'"
          >
            <h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-6">{{ currentService.title }}</h2>
            <p class="text-lg text-gray-600 dark:text-gray-400 mb-6">{{ currentService.description }}</p>
            
            <div class="mb-8">
              <h3 class="text-xl font-semibold text-gray-900 dark:text-white mb-4">What We Offer</h3>
              <ul class="space-y-3">
                <li 
                  v-for="(feature, index) in currentService.features" 
                  :key="index"
                  class="flex items-start"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-primary-600 mr-3 mt-1 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                  </svg>
                  <span class="text-gray-700 dark:text-gray-300">{{ feature }}</span>
                </li>
              </ul>
            </div>
            
            <router-link to="/contact" class="btn-primary">
              Get Started
            </router-link>
          </div>
          
          <div
            class="relative"
            v-motion
            :initial="{ opacity: 0, x: 40 }"
            :enter="{ opacity: 1, x: 0, transition: { delay: 200 } }"
            :key="currentService.id + '-image'"
          >
            <div class="absolute -top-6 -left-6 w-64 h-64 bg-primary-50 dark:bg-primary-900/20 rounded-full mix-blend-multiply dark:mix-blend-lighten filter blur-3xl opacity-70"></div>
            <img 
              :src="currentService.image" 
              :alt="currentService.title" 
              class="relative z-10 w-full h-auto rounded-2xl shadow-xl"
            />
          </div>
        </div>
      </div>
    </section>

    <!-- How We Work Section -->
    <section class="py-24 bg-white dark:bg-gray-900">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2 
            class="section-title"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            How We Work
          </h2>
          <p 
            class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Our collaborative process ensures that we deliver solutions that meet your needs and exceed your expectations.
          </p>
        </div>
        
        <div class="relative">
          <!-- Timeline -->
          <div class="hidden md:block absolute left-1/2 top-0 bottom-0 w-0.5 bg-gray-200 dark:bg-gray-700 transform -translate-x-1/2"></div>
          
          <!-- Timeline Items -->
          <div class="space-y-16">
            <!-- Item 1 -->
            <div class="relative flex flex-col md:flex-row items-center">
              <div
                class="md:w-1/2 md:pr-12 mb-8 md:mb-0 text-center md:text-right"
                v-motion
                :initial="{ opacity: 0, x: -40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
                <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-3">Initial Consultation</h3>
                <p class="text-gray-600 dark:text-gray-400">
                  We start by understanding your business, goals, and challenges through an in-depth discovery session.
                </p>
              </div>
              
              <div class="md:absolute md:left-1/2 md:transform md:-translate-x-1/2 z-10 bg-primary-600 text-white w-10 h-10 rounded-full flex items-center justify-center font-bold text-lg shadow-md">
                1
              </div>
              
              <div
                class="md:w-1/2 md:pl-12"
                v-motion
                :initial="{ opacity: 0, x: 40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
              </div>
            </div>
            
            <!-- Item 2 -->
            <div class="relative flex flex-col md:flex-row items-center">
              <div
                class="md:w-1/2 md:pr-12 text-center md:text-right order-2 md:order-1"
                v-motion
                :initial="{ opacity: 0, x: -40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
              </div>
              
              <div class="md:absolute md:left-1/2 md:transform md:-translate-x-1/2 z-10 bg-primary-600 text-white w-10 h-10 rounded-full flex items-center justify-center font-bold text-lg shadow-md order-1 md:order-2 mb-8 md:mb-0">
                2
              </div>
              
              <div
                class="md:w-1/2 md:pl-12 order-3 text-center md:text-left"
                v-motion
                :initial="{ opacity: 0, x: 40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
                <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-3">Strategy & Planning</h3>
                <p class="text-gray-600 dark:text-gray-400">
                  We develop a comprehensive strategy and project plan tailored to your specific needs and objectives.
                </p>
              </div>
            </div>
            
            <!-- Item 3 -->
            <div class="relative flex flex-col md:flex-row items-center">
              <div
                class="md:w-1/2 md:pr-12 mb-8 md:mb-0 text-center md:text-right"
                v-motion
                :initial="{ opacity: 0, x: -40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
                <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-3">Design & Development</h3>
                <p class="text-gray-600 dark:text-gray-400">
                  Our team designs and develops your solution with regular check-ins and iterative improvements based on feedback.
                </p>
              </div>
              
              <div class="md:absolute md:left-1/2 md:transform md:-translate-x-1/2 z-10 bg-primary-600 text-white w-10 h-10 rounded-full flex items-center justify-center font-bold text-lg shadow-md">
                3
              </div>
              
              <div
                class="md:w-1/2 md:pl-12"
                v-motion
                :initial="{ opacity: 0, x: 40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
              </div>
            </div>
            
            <!-- Item 4 -->
            <div class="relative flex flex-col md:flex-row items-center">
              <div
                class="md:w-1/2 md:pr-12 text-center md:text-right order-2 md:order-1"
                v-motion
                :initial="{ opacity: 0, x: -40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
              </div>
              
              <div class="md:absolute md:left-1/2 md:transform md:-translate-x-1/2 z-10 bg-primary-600 text-white w-10 h-10 rounded-full flex items-center justify-center font-bold text-lg shadow-md order-1 md:order-2 mb-8 md:mb-0">
                4
              </div>
              
              <div
                class="md:w-1/2 md:pl-12 order-3 text-center md:text-left"
                v-motion
                :initial="{ opacity: 0, x: 40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
                <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-3">Testing & Refinement</h3>
                <p class="text-gray-600 dark:text-gray-400">
                  We rigorously test every aspect of your solution to ensure it meets the highest standards of quality and performance.
                </p>
              </div>
            </div>
            
            <!-- Item 5 -->
            <div class="relative flex flex-col md:flex-row items-center">
              <div
                class="md:w-1/2 md:pr-12 mb-8 md:mb-0 text-center md:text-right"
                v-motion
                :initial="{ opacity: 0, x: -40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
                <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-3">Launch & Support</h3>
                <p class="text-gray-600 dark:text-gray-400">
                  We ensure a smooth launch and provide ongoing support to help your solution succeed in the long term.
                </p>
              </div>
              
              <div class="md:absolute md:left-1/2 md:transform md:-translate-x-1/2 z-10 bg-primary-600 text-white w-10 h-10 rounded-full flex items-center justify-center font-bold text-lg shadow-md">
                5
              </div>
              
              <div
                class="md:w-1/2 md:pl-12"
                v-motion
                :initial="{ opacity: 0, x: 40 }"
                :enter="{ opacity: 1, x: 0 }"
              >
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="py-24 bg-gradient-to-r from-primary-600 to-secondary-700 relative overflow-hidden">
      <div class="absolute inset-0 opacity-10">
        <div class="absolute -top-24 -right-24 w-96 h-96 bg-white rounded-full"></div>
        <div class="absolute -bottom-24 -left-24 w-96 h-96 bg-white rounded-full"></div>
      </div>
      
      <div class="container-custom relative z-10">
        <div class="max-w-4xl mx-auto text-center">
          <h2 
            class="text-3xl sm:text-4xl font-bold text-white mb-6"
            v-motion
            :initial="{ opacity: 0, scale: 0.9 }"
            :enter="{ opacity: 1, scale: 1 }"
          >
            Ready to get started?
          </h2>
          <p 
            class="text-lg text-white/90 mb-10 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 20 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Let's discuss how we can help you achieve your digital goals and take your business to the next level.
          </p>
          <router-link 
            to="/contact" 
            class="inline-flex items-center justify-center px-8 py-4 border border-transparent text-base font-medium rounded-md text-primary-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-primary-700 focus:ring-white transition-all duration-300"
            v-motion
            :initial="{ opacity: 0, y: 20 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 400 } }"
          >
            Get in Touch
          </router-link>
        </div>
      </div>
    </section>
  </div>
</template>