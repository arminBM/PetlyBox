<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const slides = [
  {
    image: 'path_to_image_1.jpg',
    title: "Your Pet's Joy, Delivered Every Month",
    subtitle: 'A totally customized box of themed toys and treats for your Pet - every month'
  },
  {
    image: 'path_to_image_2.jpg',
    title: 'Surprise Toys & Treats Every Month',
    subtitle: 'Handpicked goodies to make your pet happy and healthy'
  },
  {
    image: 'path_to_image_3.jpg',
    title: 'Join the PetlyBox Family Today',
    subtitle: 'Monthly fun, delivered straight to your door'
  }
]

const currentIndex = ref(0)
let interval = null

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % slides.length
}

const goToSlide = (index) => {
  currentIndex.value = index
  resetInterval()
}

const startInterval = () => {
  interval = setInterval(nextSlide, 5000)
}

const resetInterval = () => {
  clearInterval(interval)
  startInterval()
}

onMounted(() => {
  startInterval()
})

onUnmounted(() => {
  clearInterval(interval)
})

const handleClick = () => {
  alert('Button clicked!');
};
</script>

<template>
  <section class="relative h-screen overflow-hidden">
    <div
      v-for="(slide, index) in slides"
      :key="index"
      class="absolute inset-0 bg-cover bg-center transition-opacity duration-1000"
      :style="{ backgroundImage: `url(${slide.image})`, opacity: currentIndex === index ? 1 : 0 }"
    >
      <div class="absolute inset-0 bg-black opacity-50"></div>
      <div class="relative z-10 flex items-center justify-center h-full text-center text-white px-4">
        <div>
          <h1 class="text-4xl font-bold mb-4">{{ slide.title }}</h1>
          <p class="text-xl mb-6">{{ slide.subtitle }}</p>
          <button class="bg-yellow-500 text-black py-2 px-6 rounded-full">Get PetlyBox</button>
        </div>
      </div>
    </div>

    <div
      class="absolute bottom-6 left-1/2 transform -translate-x-1/2 flex gap-3 z-20"
    >
      <button
        v-for="(slide, index) in slides"
        :key="index"
        @click="goToSlide(index)"
        :class="[
          'w-4 h-4 rounded-full cursor-pointer transition-all focus:outline-none',
          currentIndex === index ? 'bg-yellow-500 scale-125' : 'bg-white'
        ]"
      ></button>
    </div>
  </section>
</template>