<script setup>
import { ref, computed, onMounted } from "vue";
import { useMotion } from "@vueuse/motion";
import gsap from "gsap";

const teamMembers = [
  {
    name: "Sarah Johnson",
    role: "CEO & Founder",
    bio: "With over 15 years of experience in digital innovation, Sarah leads our vision and strategy.",
    image:
      "https://images.pexels.com/photos/1181686/pexels-photo-1181686.jpeg?auto=compress&cs=tinysrgb&h=350",
  },
  {
    name: "Michael Chen",
    role: "Lead Developer",
    bio: "Michael is an expert in front-end and back-end technologies with a passion for creating intuitive user experiences.",
    image:
      "https://images.pexels.com/photos/2379004/pexels-photo-2379004.jpeg?auto=compress&cs=tinysrgb&h=350",
  },
  {
    name: "Emma Rodriguez",
    role: "Design Director",
    bio: "Emma combines artistic vision with technical expertise to create stunning, functional designs.",
    image:
      "https://images.pexels.com/photos/3796217/pexels-photo-3796217.jpeg?auto=compress&cs=tinysrgb&h=350",
  },
  {
    name: "David Kim",
    role: "Project Manager",
    bio: "David ensures our projects run smoothly, delivering exceptional results on time and within budget.",
    image:
      "https://images.pexels.com/photos/3785079/pexels-photo-3785079.jpeg?auto=compress&cs=tinysrgb&h=350",
  },
];

const values = [
  {
    title: "Innovation",
    description:
      "We push the boundaries of what's possible, embracing new technologies and creative approaches.",
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z" /></svg>`,
  },
  {
    title: "Excellence",
    description:
      "We strive for excellence in everything we do, from code quality to design aesthetics to client service.",
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z" /></svg>`,
  },
  {
    title: "Collaboration",
    description:
      "We believe in the power of teamwork and partnership, both within our team and with our clients.",
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" /></svg>`,
  },
  {
    title: "Integrity",
    description:
      "We operate with honesty, transparency, and respect in all our interactions and business practices.",
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" /></svg>`,
  },
];

const stats = [
  { number: "10+", label: "Years Experience" },
  { number: "200+", label: "Projects Completed" },
  { number: "50+", label: "Happy Clients" },
  { number: "15", label: "Team Members" },
];

const headerRef = ref(null);

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
    },
  },
});

onMounted(() => {
  // Animate numbers with counter effect
  const statNumbers = document.querySelectorAll(".stat-number");

  statNumbers.forEach((el) => {
    const value = el.textContent;
    el.textContent = "0";

    gsap.to(el, {
      innerText: value,
      duration: 2,
      ease: "power2.out",
      snap: { innerText: 1 },
      scrollTrigger: {
        trigger: el,
        start: "top 90%",
      },
    });
  });
});
</script>

<template>
  <div>
    <!-- Hero Section -->
    <section
      class="relative pt-24 pb-16 overflow-hidden bg-white dark:bg-gray-900"
    >
      <div class="container-custom py-16">
        <div ref="headerRef" class="max-w-3xl mx-auto text-center">
          <h1
            class="text-4xl md:text-5xl font-bold tracking-tight text-gray-900 dark:text-white mb-6"
          >
            About VisionTech
          </h1>
          <p class="text-lg text-gray-600 dark:text-gray-300 mb-6">
            We're a team of passionate designers, developers, and strategists
            who love creating exceptional digital experiences that transform
            businesses.
          </p>
        </div>
      </div>
    </section>

    <!-- Mission Section -->
    <section class="py-16 bg-gray-50 dark:bg-gray-950">
      <div class="container-custom">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
          <div
            v-motion
            :initial="{ opacity: 0, x: -40 }"
            :enter="{ opacity: 1, x: 0 }"
          >
            <h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-6">
              Our Mission
            </h2>
            <p class="text-lg text-gray-600 dark:text-gray-400 mb-6">
              At VisionTech, our mission is to empower businesses through
              innovative digital solutions that drive growth and create
              meaningful connections with their audience.
            </p>
            <p class="text-lg text-gray-600 dark:text-gray-400 mb-6">
              We believe in the transformative power of technology when aligned
              with strategic creativity and user-centered design. Our approach
              combines technical expertise with creative thinking to deliver
              solutions that not only solve problems but elevate brands to new
              heights.
            </p>
            <p class="text-lg text-gray-600 dark:text-gray-400">
              Every project we undertake is driven by our commitment to
              excellence, innovation, and delivering measurable results for our
              clients.
            </p>
          </div>

          <div
            class="relative"
            v-motion
            :initial="{ opacity: 0, x: 40 }"
            :enter="{ opacity: 1, x: 0, transition: { delay: 200 } }"
          >
            <div
              class="absolute -top-6 -left-6 w-72 h-72 bg-primary-50 dark:bg-primary-900/20 rounded-full mix-blend-multiply dark:mix-blend-lighten filter blur-3xl opacity-70"
            ></div>
            <img
              src="https://images.pexels.com/photos/3184291/pexels-photo-3184291.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260"
              alt="Our team collaborating"
              class="relative z-10 w-full h-auto rounded-2xl shadow-xl"
            />
          </div>
        </div>
      </div>
    </section>

    <!-- Values Section -->
    <section id="values" class="py-24 bg-white dark:bg-gray-900">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2
            class="section-title"
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            Our Values
          </h2>
          <p
            class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            These core values guide everything we do, from how we work together
            as a team to how we approach every client project.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(value, index) in values"
            :key="index"
            class="card p-6 hover:translate-y-[-8px]"
          >
            <div
              class="h-12 w-12 flex items-center justify-center rounded-md bg-primary-100 dark:bg-primary-900/30 text-primary-600 dark:text-primary-400 mb-5"
            >
              <span v-html="value.icon"></span>
            </div>
            <h3
              class="text-xl font-semibold text-gray-900 dark:text-white mb-3"
            >
              {{ value.title }}
            </h3>
            <p class="text-gray-600 dark:text-gray-400">
              {{ value.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Section -->
    <section class="py-20 bg-primary-600">
      <div class="container-custom">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8 text-center">
          <div
            v-for="(stat, index) in stats"
            :key="index"
            class="transform transition-transform duration-500 hover:scale-105"
          >
            <div
              class="stat-number text-4xl md:text-5xl font-bold text-white mb-2"
            >
              {{ stat.number }}
            </div>
            <div class="text-primary-100 text-lg">{{ stat.label }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Team Section -->
    <section id="team" class="py-24 bg-gray-50 dark:bg-gray-950">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2
            class="section-title"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            Meet Our Team
          </h2>
          <p
            class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            We're a diverse team of talented individuals passionate about
            creating exceptional digital experiences.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(member, index) in teamMembers"
            :key="index"
            class="card overflow-hidden group"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{
              opacity: 1,
              y: 0,
              transition: { delay: index * 100 + 400 },
            }"
          >
            <div class="relative h-64 overflow-hidden">
              <img
                :src="member.image"
                :alt="member.name"
                class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
              />
            </div>
            <div class="p-6">
              <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
                {{ member.name }}
              </h3>
              <p class="text-primary-600 dark:text-primary-400 mb-3">
                {{ member.role }}
              </p>
              <p class="text-gray-600 dark:text-gray-400">{{ member.bio }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="relative py-20 bg-white dark:bg-gray-900 overflow-hidden">
      <div
        class="absolute right-0 bottom-0 w-1/3 h-full bg-primary-50 dark:bg-primary-900/20 clip-path-slant"
      ></div>
      <div class="container-custom relative z-10">
        <div class="max-w-3xl mx-auto text-center">
          <h2
            class="text-3xl font-bold text-gray-900 dark:text-white mb-6"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            Ready to Work With Us?
          </h2>
          <p
            class="text-lg text-gray-600 dark:text-gray-400 mb-8"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Let's discuss how we can help you achieve your digital goals.
          </p>
          <router-link
            to="/contact"
            class="btn-primary"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 400 } }"
          >
            Get in Touch
          </router-link>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.clip-path-slant {
  clip-path: polygon(100% 0, 100% 100%, 0 100%);
}
</style>
