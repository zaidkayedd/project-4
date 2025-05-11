<script setup>
import { onMounted, ref } from 'vue';
import { useMotion } from '@vueuse/motion';
import gsap from 'gsap';
import FeatureCard from '../components/home/FeatureCard.vue';
import TestimonialCard from '../components/home/TestimonialCard.vue';
import LogoCloud from '../components/home/LogoCloud.vue';
import ProjectCard from '../components/projects/ProjectCard.vue';

const heroRef = ref(null);
const heroTitle = ref(null);
const heroSubtitle = ref(null);
const heroCta = ref(null);
const heroImage = ref(null);

const features = [
  {
    title: 'Web Development',
    description: 'We build custom web applications with modern technologies that deliver exceptional user experiences.',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" /></svg>`
  },
  {
    title: 'UI/UX Design',
    description: 'Our design team creates intuitive, beautiful interfaces that engage users and elevate your brand.',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zm0 0h12a2 2 0 002-2v-4a2 2 0 00-2-2h-2.343M11 7.343l1.657-1.657a2 2 0 012.828 0l2.829 2.829a2 2 0 010 2.828l-8.486 8.485M7 17h.01" /></svg>`
  },
  {
    title: 'Mobile Apps',
    description: 'We develop cross-platform mobile applications that work seamlessly across iOS and Android devices.',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" /></svg>`
  },
  {
    title: 'Digital Marketing',
    description: 'Our strategic marketing services help you reach your target audience and drive meaningful conversions.',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 3.055A9.001 9.001 0 1020.945 13H11V3.055z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.488 9H15V3.512A9.025 9.025 0 0120.488 9z" /></svg>`
  }
];

const testimonials = [
  {
    quote: "VisionTech transformed our outdated website into a modern, high-converting platform that perfectly represents our brand.",
    author: "Sarah Johnson",
    role: "CEO, TechFlow Inc.",
    image: "https://images.pexels.com/photos/1181686/pexels-photo-1181686.jpeg?auto=compress&cs=tinysrgb&h=150"
  },
  {
    quote: "The team at VisionTech went above and beyond to deliver our mobile app. Their attention to detail and commitment to quality is unmatched.",
    author: "Michael Chen",
    role: "Founder, Novus",
    image: "https://images.pexels.com/photos/2379004/pexels-photo-2379004.jpeg?auto=compress&cs=tinysrgb&h=150"
  },
  {
    quote: "Working with VisionTech has been a game-changer for our business. Their strategic approach to digital marketing has helped us scale rapidly.",
    author: "Emma Rodriguez",
    role: "Marketing Director, Elevate",
    image: "https://images.pexels.com/photos/3796217/pexels-photo-3796217.jpeg?auto=compress&cs=tinysrgb&h=150"
  }
];

const featuredProjects = [
  {
    title: "Novus E-commerce Platform",
    description: "A modern e-commerce platform with advanced filtering, real-time inventory, and personalized recommendations.",
    image: "https://images.pexels.com/photos/6956903/pexels-photo-6956903.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "Web Development",
    link: "/projects"
  },
  {
    title: "Elevate Mobile App",
    description: "A fitness tracking app with personalized workout plans, progress tracking, and social features.",
    image: "https://images.pexels.com/photos/3912990/pexels-photo-3912990.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "Mobile Development",
    link: "/projects"
  },
  {
    title: "TechFlow Dashboard",
    description: "An intuitive admin dashboard with real-time analytics, customizable widgets, and data visualization.",
    image: "https://images.pexels.com/photos/4050315/pexels-photo-4050315.jpeg?auto=compress&cs=tinysrgb&h=350",
    category: "UI/UX Design",
    link: "/projects"
  }
];

const heroMotion = useMotion(heroRef, {
  initial: { opacity: 0 },
  visible: { opacity: 1, transition: { duration: 800 } },
});

onMounted(() => {
  const tl = gsap.timeline();
  
  // Hero animations
  tl.from(heroTitle.value, {
    opacity: 0,
    y: 50,
    duration: 0.8,
    ease: "power3.out"
  })
  .from(heroSubtitle.value, {
    opacity: 0,
    y: 30,
    duration: 0.8,
    ease: "power3.out"
  }, "-=0.6")
  .from(heroCta.value, {
    opacity: 0,
    y: 30,
    duration: 0.8,
    ease: "power3.out"
  }, "-=0.6")
  .from(heroImage.value, {
    opacity: 0,
    scale: 0.9,
    duration: 1,
    ease: "power3.out"
  }, "-=0.8");
  
  // Animate background gradient
  const heroGradient = document.querySelector('.hero-gradient');
  if (heroGradient) {
    gsap.to(heroGradient, {
      background: 'radial-gradient(circle at 60% 60%, rgba(99, 102, 241, 0.15), rgba(139, 92, 246, 0.05))',
      duration: 10,
      repeat: -1,
      yoyo: true,
      ease: "sine.inOut"
    });
  }
});
</script>

<template>
  <div>
    <!-- Hero Section -->
    <section 
      ref="heroRef"
      class="relative pt-24 pb-16 overflow-hidden bg-white dark:bg-gray-900 hero-gradient"
    >
      <div class="absolute inset-0 bg-grid"></div>
      <div class="container-custom relative z-10 pt-12 pb-24 md:pt-16 md:pb-32">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
          <div class="lg:col-span-6">
            <h1 
              ref="heroTitle"
              class="text-4xl md:text-5xl lg:text-6xl font-bold tracking-tight text-gray-900 dark:text-white mb-6"
            >
              Transforming Ideas Into 
              <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary-500 to-secondary-600">
                Digital Excellence
              </span>
            </h1>
            <p 
              ref="heroSubtitle"
              class="text-lg md:text-xl text-gray-600 dark:text-gray-300 mb-8 max-w-2xl"
            >
              We create stunning digital experiences that elevate your brand and drive results. 
              Our team of experts combines cutting-edge technology with beautiful design to deliver 
              solutions that stand out.
            </p>
            <div ref="heroCta" class="flex flex-col sm:flex-row gap-4">
              <router-link to="/contact" class="btn-primary">
                Get Started
              </router-link>
              <router-link to="/projects" class="btn-outline">
                View Our Work
              </router-link>
            </div>
          </div>
          <div class="lg:col-span-6 flex justify-center">
            <div 
              ref="heroImage"
              class="relative w-full max-w-lg"
            >
              <!-- Abstract shapes for visual interest -->
              <div class="absolute -top-12 -left-12 w-72 h-72 bg-primary-50 dark:bg-primary-900/20 rounded-full mix-blend-multiply dark:mix-blend-lighten filter blur-3xl opacity-70 animate-pulse-slow"></div>
              <div class="absolute -bottom-12 -right-12 w-72 h-72 bg-secondary-50 dark:bg-secondary-900/20 rounded-full mix-blend-multiply dark:mix-blend-lighten filter blur-3xl opacity-70 animate-pulse-slow animation-delay-2000"></div>
              <div class="absolute inset-x-16 -bottom-20 w-80 h-80 bg-accent-50 dark:bg-accent-900/20 rounded-full mix-blend-multiply dark:mix-blend-lighten filter blur-3xl opacity-70 animate-pulse-slow animation-delay-4000"></div>
              
              <!-- Hero image -->
              <img 
                src="https://images.pexels.com/photos/3861969/pexels-photo-3861969.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260" 
                alt="Digital workspace with laptop and creative elements"
                class="relative z-10 w-full h-auto rounded-2xl shadow-2xl"
              />
            </div>
          </div>
        </div>
      </div>
      
      <!-- Hero wave divider -->
      <div class="absolute bottom-0 left-0 right-0">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 160" class="w-full h-auto fill-gray-50 dark:fill-gray-950">
          <path d="M0,160L40,138.7C80,117,160,75,240,64C320,53,400,75,480,96C560,117,640,139,720,138.7C800,139,880,117,960,90.7C1040,64,1120,32,1200,32C1280,32,1360,64,1400,80L1440,96L1440,160L1400,160C1360,160,1280,160,1200,160C1120,160,1040,160,960,160C880,160,800,160,720,160C640,160,560,160,480,160C400,160,320,160,240,160C160,160,80,160,40,160L0,160Z"></path>
        </svg>
      </div>
    </section>

    <!-- Features Section -->
    <section class="py-24 bg-gray-50 dark:bg-gray-950">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2 
            class="section-title"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Our Services
          </h2>
          <p 
            class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 400 } }"
          >
            We offer a comprehensive range of digital services to help your business thrive in the digital world.
          </p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <FeatureCard 
            v-for="(feature, index) in features" 
            :key="index" 
            :title="feature.title" 
            :description="feature.description" 
            :icon="feature.icon"
            :delay="index * 100 + 500"
          />
        </div>
      </div>
    </section>

    <!-- About/CTA Section with diagonal design -->
    <section class="diagonal-box">
      <div class="container-custom py-24">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2 
            class="section-title"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            Why Choose Us
          </h2>
        </div>
        
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
          <div>
            <div 
              class="relative aspect-video rounded-2xl overflow-hidden shadow-xl"
              v-motion
              :initial="{ opacity: 0, x: -40 }"
              :enter="{ opacity: 1, x: 0, transition: { delay: 200 } }"
            >
              <img 
                src="https://images.pexels.com/photos/3182812/pexels-photo-3182812.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260" 
                alt="Team collaboration" 
                class="w-full h-full object-cover"
              />
            </div>
          </div>
          
          <div
            v-motion
            :initial="{ opacity: 0, x: 40 }"
            :enter="{ opacity: 1, x: 0, transition: { delay: 400 } }"
          >
            <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-6">
              We're more than just developers and designers
            </h3>
            <p class="text-gray-600 dark:text-gray-400 mb-6">
              At VisionTech, we believe in creating digital experiences that not only look stunning but also drive real business results. Our team of experts is passionate about pushing the boundaries of what's possible on the web.
            </p>
            <ul class="space-y-4 mb-8">
              <li class="flex">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600 mr-3 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
                <span class="text-gray-700 dark:text-gray-300">Dedicated team of expert developers and designers</span>
              </li>
              <li class="flex">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600 mr-3 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
                <span class="text-gray-700 dark:text-gray-300">Results-driven approach focused on your business goals</span>
              </li>
              <li class="flex">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600 mr-3 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
                <span class="text-gray-700 dark:text-gray-300">Cutting-edge technology and proven strategies</span>
              </li>
              <li class="flex">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600 mr-3 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
                <span class="text-gray-700 dark:text-gray-300">Transparent communication and collaborative process</span>
              </li>
            </ul>
            <router-link to="/about" class="btn-primary">
              Learn More About Us
            </router-link>
          </div>
        </div>
      </div>
    </section>

    <!-- Logo Cloud Section -->
    <section class="py-16 bg-white dark:bg-gray-900">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-12">
          <h2 
            class="text-xl font-semibold text-gray-900 dark:text-white mb-4"
            v-motion
            :initial="{ opacity: 0, y: 20 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            Trusted by industry-leading companies
          </h2>
        </div>
        
        <LogoCloud />
      </div>
    </section>

    <!-- Featured Projects -->
    <section class="py-24 bg-gray-50 dark:bg-gray-950">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2 
            class="section-title"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            Our Featured Projects
          </h2>
          <p 
            class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Take a look at some of our recent work that has made a real impact for our clients.
          </p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <ProjectCard 
            v-for="(project, index) in featuredProjects" 
            :key="index" 
            :title="project.title" 
            :description="project.description"
            :image="project.image"
            :category="project.category"
            :link="project.link"
            :delay="index * 100 + 400"
          />
        </div>
        
        <div class="text-center mt-12">
          <router-link to="/projects" class="btn-primary">
            View All Projects
          </router-link>
        </div>
      </div>
    </section>

    <!-- Testimonials -->
    <section class="py-24 bg-white dark:bg-gray-900">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2 
            class="section-title"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            What Our Clients Say
          </h2>
          <p 
            class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Don't just take our word for it. Here's what some of our clients have to say about working with us.
          </p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <TestimonialCard 
            v-for="(testimonial, index) in testimonials" 
            :key="index" 
            :quote="testimonial.quote"
            :author="testimonial.author"
            :role="testimonial.role"
            :image="testimonial.image"
            :delay="index * 100 + 400"
          />
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
            Ready to transform your digital presence?
          </h2>
          <p 
            class="text-lg text-white/90 mb-10 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 20 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Let's discuss how we can help you achieve your goals and take your business to the next level.
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