<script setup>
import { ref } from 'vue';
import { useMotion } from '@vueuse/motion';

const headerRef = ref(null);
const formSubmitted = ref(false);
const formError = ref(false);

const formData = ref({
  name: '',
  email: '',
  phone: '',
  service: '',
  message: ''
});

const serviceOptions = [
  { value: '', label: 'Select a service' },
  { value: 'web-development', label: 'Web Development' },
  { value: 'ui-ux-design', label: 'UI/UX Design' },
  { value: 'mobile-development', label: 'Mobile Development' },
  { value: 'digital-marketing', label: 'Digital Marketing' },
  { value: 'other', label: 'Other' }
];

const handleSubmit = () => {
  // Validate form
  if (!formData.value.name || !formData.value.email || !formData.value.message) {
    formError.value = true;
    return;
  }
  
  // In a real app, this would send the form data to a server
  console.log('Form submitted:', formData.value);
  
  // Reset form
  formSubmitted.value = true;
  formError.value = false;
  formData.value = {
    name: '',
    email: '',
    phone: '',
    service: '',
    message: ''
  };
  
  // Reset success message after 5 seconds
  setTimeout(() => {
    formSubmitted.value = false;
  }, 5000);
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
            Get in Touch
          </h1>
          <p class="text-lg text-gray-600 dark:text-gray-300 mb-6">
            Have a project in mind or want to learn more about our services?
            We'd love to hear from you. Fill out the form below and we'll get back to you as soon as possible.
          </p>
        </div>
      </div>
    </section>

    <!-- Contact Form Section -->
    <section class="py-24 bg-gray-50 dark:bg-gray-950">
      <div class="container-custom">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16">
          <!-- Contact Form -->
          <div
            v-motion
            :initial="{ opacity: 0, x: -40 }"
            :enter="{ opacity: 1, x: 0 }"
          >
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-8">
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-6">Send Us a Message</h2>
              
              <div v-if="formSubmitted" class="mb-6 p-4 bg-green-100 dark:bg-green-800 text-green-800 dark:text-green-100 rounded-md">
                <p>Thank you for your message! We'll get back to you soon.</p>
              </div>
              
              <div v-if="formError" class="mb-6 p-4 bg-red-100 dark:bg-red-800 text-red-800 dark:text-red-100 rounded-md">
                <p>Please fill out all required fields.</p>
              </div>
              
              <form @submit.prevent="handleSubmit" class="space-y-6">
                <div>
                  <label for="name" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
                    Name <span class="text-red-600">*</span>
                  </label>
                  <input
                    type="text"
                    id="name"
                    v-model="formData.name"
                    required
                    class="w-full px-4 py-2 border border-gray-300 dark:border-gray-700 rounded-md focus:outline-none focus:ring-2 focus:ring-primary-500 focus:border-primary-500 dark:bg-gray-700 dark:text-white"
                  />
                </div>
                
                <div>
                  <label for="email" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
                    Email <span class="text-red-600">*</span>
                  </label>
                  <input
                    type="email"
                    id="email"
                    v-model="formData.email"
                    required
                    class="w-full px-4 py-2 border border-gray-300 dark:border-gray-700 rounded-md focus:outline-none focus:ring-2 focus:ring-primary-500 focus:border-primary-500 dark:bg-gray-700 dark:text-white"
                  />
                </div>
                
                <div>
                  <label for="phone" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
                    Phone
                  </label>
                  <input
                    type="tel"
                    id="phone"
                    v-model="formData.phone"
                    class="w-full px-4 py-2 border border-gray-300 dark:border-gray-700 rounded-md focus:outline-none focus:ring-2 focus:ring-primary-500 focus:border-primary-500 dark:bg-gray-700 dark:text-white"
                  />
                </div>
                
                <div>
                  <label for="service" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
                    Service You're Interested In
                  </label>
                  <select
                    id="service"
                    v-model="formData.service"
                    class="w-full px-4 py-2 border border-gray-300 dark:border-gray-700 rounded-md focus:outline-none focus:ring-2 focus:ring-primary-500 focus:border-primary-500 dark:bg-gray-700 dark:text-white"
                  >
                    <option 
                      v-for="option in serviceOptions" 
                      :key="option.value" 
                      :value="option.value"
                    >
                      {{ option.label }}
                    </option>
                  </select>
                </div>
                
                <div>
                  <label for="message" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
                    Message <span class="text-red-600">*</span>
                  </label>
                  <textarea
                    id="message"
                    v-model="formData.message"
                    required
                    rows="5"
                    class="w-full px-4 py-2 border border-gray-300 dark:border-gray-700 rounded-md focus:outline-none focus:ring-2 focus:ring-primary-500 focus:border-primary-500 dark:bg-gray-700 dark:text-white"
                  ></textarea>
                </div>
                
                <div>
                  <button
                    type="submit"
                    class="btn-primary w-full"
                  >
                    Send Message
                  </button>
                </div>
              </form>
            </div>
          </div>
          
          <!-- Contact Info -->
          <div
            v-motion
            :initial="{ opacity: 0, x: 40 }"
            :enter="{ opacity: 1, x: 0, transition: { delay: 200 } }"
          >
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-8 h-full">
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-6">Contact Information</h2>
              
              <div class="space-y-6">
                <div class="flex items-start">
                  <div class="flex-shrink-0 h-10 w-10 rounded-full bg-primary-100 dark:bg-primary-900/30 flex items-center justify-center text-primary-600 dark:text-primary-400">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                    </svg>
                  </div>
                  <div class="ml-4">
                    <h3 class="text-lg font-medium text-gray-900 dark:text-white">Phone</h3>
                    <p class="mt-1 text-gray-600 dark:text-gray-400">+1 (555) 123-4567</p>
                  </div>
                </div>
                
                <div class="flex items-start">
                  <div class="flex-shrink-0 h-10 w-10 rounded-full bg-primary-100 dark:bg-primary-900/30 flex items-center justify-center text-primary-600 dark:text-primary-400">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                    </svg>
                  </div>
                  <div class="ml-4">
                    <h3 class="text-lg font-medium text-gray-900 dark:text-white">Email</h3>
                    <p class="mt-1 text-gray-600 dark:text-gray-400">info@visiontech.com</p>
                  </div>
                </div>
                
                <div class="flex items-start">
                  <div class="flex-shrink-0 h-10 w-10 rounded-full bg-primary-100 dark:bg-primary-900/30 flex items-center justify-center text-primary-600 dark:text-primary-400">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                    </svg>
                  </div>
                  <div class="ml-4">
                    <h3 class="text-lg font-medium text-gray-900 dark:text-white">Address</h3>
                    <p class="mt-1 text-gray-600 dark:text-gray-400">
                      123 Innovation Street<br>
                      San Francisco, CA 94103<br>
                      United States
                    </p>
                  </div>
                </div>
              </div>
              
              <div class="mt-12">
                <h3 class="text-lg font-medium text-gray-900 dark:text-white mb-4">Follow Us</h3>
                <div class="flex space-x-4">
                  <a href="#" class="text-gray-500 hover:text-gray-900 dark:text-gray-400 dark:hover:text-white">
                    <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                      <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd" />
                    </svg>
                  </a>
                  <a href="#" class="text-gray-500 hover:text-gray-900 dark:text-gray-400 dark:hover:text-white">
                    <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                      <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd" />
                    </svg>
                  </a>
                  <a href="#" class="text-gray-500 hover:text-gray-900 dark:text-gray-400 dark:hover:text-white">
                    <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                      <path d="M8.29 20.251c7.547 0 11.675-6.253 11.675-11.675 0-.178 0-.355-.012-.53A8.348 8.348 0 0022 5.92a8.19 8.19 0 01-2.357.646 4.118 4.118 0 001.804-2.27 8.224 8.224 0 01-2.605.996 4.107 4.107 0 00-6.993 3.743 11.65 11.65 0 01-8.457-4.287 4.106 4.106 0 001.27 5.477A4.072 4.072 0 012.8 9.713v.052a4.105 4.105 0 003.292 4.022 4.095 4.095 0 01-1.853.07 4.108 4.108 0 003.834 2.85A8.233 8.233 0 012 18.407a11.616 11.616 0 006.29 1.84" />
                    </svg>
                  </a>
                  <a href="#" class="text-gray-500 hover:text-gray-900 dark:text-gray-400 dark:hover:text-white">
                    <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                      <path fill-rule="evenodd" d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z" clip-rule="evenodd" />
                    </svg>
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Map Section -->
    <section class="py-16 bg-white dark:bg-gray-900">
      <div class="container-custom">
        <div 
          class="rounded-lg overflow-hidden shadow-xl"
          v-motion
          :initial="{ opacity: 0, y: 40 }"
          :enter="{ opacity: 1, y: 0 }"
        >
          <iframe 
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3153.7462606490187!2d-122.41941722393326!3d37.77492971584182!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x80858080c46e7fc7%3A0x5f4bd4d883e89d92!2sSan%20Francisco%2C%20CA%2094103!5e0!3m2!1sen!2sus!4v1695299133029!5m2!1sen!2sus" 
            width="100%" 
            height="450" 
            style="border:0;" 
            allowfullscreen="" 
            loading="lazy" 
            referrerpolicy="no-referrer-when-downgrade"
          ></iframe>
        </div>
      </div>
    </section>

    <!-- FAQ Section -->
    <section class="py-24 bg-gray-50 dark:bg-gray-950">
      <div class="container-custom">
        <div class="max-w-3xl mx-auto text-center mb-16">
          <h2 
            class="section-title"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0 }"
          >
            Frequently Asked Questions
          </h2>
          <p 
            class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto"
            v-motion
            :initial="{ opacity: 0, y: 40 }"
            :enter="{ opacity: 1, y: 0, transition: { delay: 200 } }"
          >
            Find answers to common questions about our services and processes.
          </p>
        </div>
        
        <div class="max-w-3xl mx-auto">
          <div class="space-y-6">
            <div 
              class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6"
              v-motion
              :initial="{ opacity: 0, y: 20 }"
              :enter="{ opacity: 1, y: 0, transition: { delay: 300 } }"
            >
              <h3 class="text-xl font-semibold text-gray-900 dark:text-white mb-3">What services do you offer?</h3>
              <p class="text-gray-600 dark:text-gray-400">
                We offer a comprehensive range of digital services, including web development, UI/UX design, mobile app development, and digital marketing. Our team specializes in creating custom solutions tailored to your specific needs.
              </p>
            </div>
            
            <div 
              class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6"
              v-motion
              :initial="{ opacity: 0, y: 20 }"
              :enter="{ opacity: 1, y: 0, transition: { delay: 400 } }"
            >
              <h3 class="text-xl font-semibold text-gray-900 dark:text-white mb-3">How much does a typical project cost?</h3>
              <p class="text-gray-600 dark:text-gray-400">
                Project costs vary depending on the scope, complexity, and specific requirements. We work with clients of all sizes and budgets. After our initial consultation, we'll provide a detailed proposal with transparent pricing.
              </p>
            </div>
            
            <div 
              class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6"
              v-motion
              :initial="{ opacity: 0, y: 20 }"
              :enter="{ opacity: 1, y: 0, transition: { delay: 500 } }"
            >
              <h3 class="text-xl font-semibold text-gray-900 dark:text-white mb-3">How long does a typical project take?</h3>
              <p class="text-gray-600 dark:text-gray-400">
                Timeline depends on the project scope and complexity. A simple website might take 4-6 weeks, while a complex web application could take 3-6 months. We'll provide a detailed timeline during our project planning phase.
              </p>
            </div>
            
            <div 
              class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6"
              v-motion
              :initial="{ opacity: 0, y: 20 }"
              :enter="{ opacity: 1, y: 0, transition: { delay: 600 } }"
            >
              <h3 class="text-xl font-semibold text-gray-900 dark:text-white mb-3">Do you offer ongoing support and maintenance?</h3>
              <p class="text-gray-600 dark:text-gray-400">
                Yes, we offer various support and maintenance packages to ensure your digital solutions continue to perform optimally. These can include regular updates, security monitoring, performance optimization, and technical support.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>