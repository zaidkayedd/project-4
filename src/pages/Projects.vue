<script setup>
import { ref, computed } from 'vue';
import { useMotion } from '@vueuse/motion';
import ProjectCard from '../components/projects/ProjectCard.vue';

const headerRef = ref(null);

const categories = [
  'All',
  'Web Development',
  'Mobile Development',
  'UI/UX Design',
  'E-commerce',
  'Digital Marketing'
];

const selectedCategory = ref('All');

const projects = [
  {
    title: "Novus E-commerce Platform",
    description: "A modern e-commerce platform with advanced filtering, real-time inventory, and personalized recommendations.",
    image: "https://images.pexels.com/photos/6956903/pexels-photo-6956903.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "E-commerce",
    link: "#"
  },
  {
    title: "Elevate Mobile App",
    description: "A fitness tracking app with personalized workout plans, progress tracking, and social features.",
    image: "https://images.pexels.com/photos/3912990/pexels-photo-3912990.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "Mobile Development",
    link: "#"
  },
  {
    title: "TechFlow Dashboard",
    description: "An intuitive admin dashboard with real-time analytics, customizable widgets, and data visualization.",
    image: "https://images.pexels.com/photos/4050315/pexels-photo-4050315.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "UI/UX Design",
    link: "#"
  },
  {
    title: "Bloom E-commerce Website",
    description: "A beautiful online store for a boutique plant shop with intuitive navigation and secure checkout.",
    image: "https://images.pexels.com/photos/4498362/pexels-photo-4498362.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "E-commerce",
    link: "#"
  },
  {
    title: "Nexus Social Platform",
    description: "A community-focused social media platform that connects like-minded individuals and groups.",
    image: "https://images.pexels.com/photos/3194519/pexels-photo-3194519.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "Web Development",
    link: "#"
  },
  {
    title: "Horizon Marketing Campaign",
    description: "A comprehensive digital marketing strategy that increased brand awareness and conversions by 200%.",
    image: "https://images.pexels.com/photos/7691714/pexels-photo-7691714.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "Digital Marketing",
    link: "#"
  },
  {
    title: "Vertex Financial App",
    description: "A secure mobile banking application with budgeting tools, investment tracking, and automated savings.",
    image: "https://images.pexels.com/photos/3943716/pexels-photo-3943716.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "Mobile Development",
    link: "#"
  },
  {
    title: "Pulse Healthcare Portal",
    description: "A patient-centered healthcare portal that streamlines appointment scheduling and medical record access.",
    image: "https://images.pexels.com/photos/3845810/pexels-photo-3845810.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "Web Development",
    link: "#"
  },
  {
    title: "Atlas Travel Companion",
    description: "An all-in-one travel app with itinerary planning, local recommendations, and real-time translations.",
    image: "https://images.pexels.com/photos/3769138/pexels-photo-3769138.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "UI/UX Design",
    link: "#"
  }
];

const filteredProjects = computed(() => {
  if (selectedCategory.value === 'All') {
    return projects;
  }
  return projects.filter(project => project.category === selectedCategory.value);
});

const selectCategory = (category) => {
  selectedCategory.value = category;
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
            Our Projects
          </h1>
          <p class="text-lg text-gray-600 dark:text-gray-300 mb-6">
            Explore our portfolio of work across various industries and technologies.
            Each project represents our commitment to excellence and innovation.
          </p>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section class="py-24 bg-gray-50 dark:bg-gray-950">
      <div class="container-custom">
        <!-- Category Filters -->
        <div 
          class="flex flex-wrap justify-center mb-12 gap-3"
          v-motion
          :initial="{ opacity: 0, y: 20 }"
          :enter="{ opacity: 1, y: 0 }"
        >
          <button 
            v-for="category in categories" 
            :key="category"
            @click="selectCategory(category)"
            class="px-4 py-2 rounded-md transition-colors duration-200"
            :class="selectedCategory === category 
              ? 'bg-primary-600 text-white' 
              : 'bg-white dark:bg-gray-800 text-gray-600 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700'"
          >
            {{ category }}
          </button>
        </div>
        
        <!-- Projects Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <template v-if="filteredProjects.length > 0">
            <ProjectCard 
              v-for="(project, index) in filteredProjects" 
              :key="index" 
              :title="project.title" 
              :description="project.description"
              :image="project.image"
              :category="project.category"
              :link="project.link"
              :delay="index * 100 + 200"
            />
          </template>
          <div 
            v-else 
            class="col-span-full text-center py-20"
            v-motion
            :initial="{ opacity: 0 }"
            :enter="{ opacity: 1 }"
          >
            <p class="text-xl text-gray-600 dark:text-gray-400">No projects found in this category.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Process Section -->
    <section class="py-24 bg-white dark:bg-gray-900">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2 
            class="section-title"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            Our Process
          </h2>
          <p 
            class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Here's how we approach each project to ensure exceptional results.
          </p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div 
            class="relative"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 300 } }"
          >
            <div class="card p-6 h-full">
              <div class="flex items-center mb-4">
                <div class="h-10 w-10 flex items-center justify-center rounded-full bg-primary-100 dark:bg-primary-900/30 text-primary-600 dark:text-primary-400 text-xl font-bold">
                  1
                </div>
                <div class="ml-4 text-xl font-semibold text-gray-900 dark:text-white">Discovery</div>
              </div>
              <p class="text-gray-600 dark:text-gray-400">
                We start by understanding your business, goals, audience, and challenges to define a clear project scope.
              </p>
            </div>
            <div class="hidden lg:block absolute top-1/2 right-0 transform translate-x-1/2 -translate-y-1/2 text-gray-300 dark:text-gray-700">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </div>
          </div>
          
          <div 
            class="relative"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 400 } }"
          >
            <div class="card p-6 h-full">
              <div class="flex items-center mb-4">
                <div class="h-10 w-10 flex items-center justify-center rounded-full bg-primary-100 dark:bg-primary-900/30 text-primary-600 dark:text-primary-400 text-xl font-bold">
                  2
                </div>
                <div class="ml-4 text-xl font-semibold text-gray-900 dark:text-white">Strategy</div>
              </div>
              <p class="text-gray-600 dark:text-gray-400">
                We develop a comprehensive plan tailored to your needs, outlining technology, design approach, and timeline.
              </p>
            </div>
            <div class="hidden lg:block absolute top-1/2 right-0 transform translate-x-1/2 -translate-y-1/2 text-gray-300 dark:text-gray-700">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </div>
          </div>
          
          <div 
            class="relative"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 500 } }"
          >
            <div class="card p-6 h-full">
              <div class="flex items-center mb-4">
                <div class="h-10 w-10 flex items-center justify-center rounded-full bg-primary-100 dark:bg-primary-900/30 text-primary-600 dark:text-primary-400 text-xl font-bold">
                  3
                </div>
                <div class="ml-4 text-xl font-semibold text-gray-900 dark:text-white">Creation</div>
              </div>
              <p class="text-gray-600 dark:text-gray-400">
                Our team designs and develops your solution with regular check-ins and iterative improvements based on feedback.
              </p>
            </div>
            <div class="hidden lg:block absolute top-1/2 right-0 transform translate-x-1/2 -translate-y-1/2 text-gray-300 dark:text-gray-700">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </div>
          </div>
          
          <div
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 600 } }"
          >
            <div class="card p-6 h-full">
              <div class="flex items-center mb-4">
                <div class="h-10 w-10 flex items-center justify-center rounded-full bg-primary-100 dark:bg-primary-900/30 text-primary-600 dark:text-primary-400 text-xl font-bold">
                  4
                </div>
                <div class="ml-4 text-xl font-semibold text-gray-900 dark:text-white">Launch & Support</div>
              </div>
              <p class="text-gray-600 dark:text-gray-400">
                We ensure a smooth launch and provide ongoing support and optimization to help your project succeed long-term.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="py-20 bg-primary-600">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto text-center">
          <h2 
            class="text-3xl sm:text-4xl font-bold text-white mb-6"
            v-motion
            :initial="{ opacity: 0, scale: 0.9 }"
            :enter="{ opacity: 1, scale: 1 }"
          >
            Have a project in mind?
          </h2>
          <p 
            class="text-lg text-white/90 mb-10 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 20 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Let's discuss how we can help you bring your vision to life.
          </p>
          <router-link 
            to="/contact" 
            class="inline-flex items-center justify-center px-8 py-4 border border-transparent text-base font-medium rounded-md text-primary-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-primary-700 focus:ring-white transition-all duration-300"
            v-motion
            :initial="{ opacity: 0, y: 20 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 400 } }"
          >
            Start Your Project
          </router-link>
        </div>
      </div>
    </section>
  </div>
</template>