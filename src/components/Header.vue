<script setup>
import { ref, onMounted } from 'vue'

const header = ref(null)
const menuOpen = ref(false)
let lastScrollY = window.scrollY
onMounted(() => {
  window.addEventListener('scroll', () => {
    if (!header.value) return

    if (window.scrollY > lastScrollY) {
      header.value.style.transform = 'translateY(-100%)'
    } else {
      header.value.style.transform = 'translateY(0)'
    }
    lastScrollY = window.scrollY
  })
})

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value
}
</script>

<template>
  <header
    ref="header"
    class="flex items-center justify-between px-4 w-screen h-14 bg-gray-500 text-xl font-bold text-red-500 fixed top-0 left-0 transition-transform duration-300 z-50"
  >
    <button
      @click="toggleMenu"
      class="relative w-8 h-8 flex flex-col justify-center items-center"
    >
      <span
        :class="[
          'block w-8 h-1 bg-white rounded transition-all duration-300',
          menuOpen ? 'rotate-45 translate-y-2' : ''
        ]"
      ></span>
      <span
        :class="[
          'block w-8 h-1 bg-white rounded transition-all duration-300 my-1',
          menuOpen ? 'opacity-0' : ''
        ]"
      ></span>
      <span
        :class="[
          'block w-8 h-1 bg-white rounded transition-all duration-300',
          menuOpen ? '-rotate-45 -translate-y-2' : ''
        ]"
      ></span>
    </button>

    <div>PetlyBox</div>

    <div>Login</div>
  </header>

  <transition name="slide">
    <aside
      v-if="menuOpen"
      class="fixed top-0 left-0 w-64 h-full bg-gray-800 text-white shadow-lg z-40 p-6"
    >
      <ul class="space-y-4 mt-10">
        <li><a href="#" class="hover:text-yellow-400">Home</a></li>
        <li><a href="#" class="hover:text-yellow-400">Store</a></li>
        <li><a href="#" class="hover:text-yellow-400">Chat</a></li>
        <li><a href="#" class="hover:text-yellow-400">Boxes</a></li>
        <li><a href="#" class="hover:text-yellow-400">Login</a></li>
      </ul>
    </aside>
  </transition>

  <div
    v-if="menuOpen"
    @click="toggleMenu"
    class="fixed inset-0 bg-black bg-opacity-50 z-30"
  ></div>
</template>

<style>
.slide-enter-from {
  transform: translateX(-100%);
}
.slide-enter-to {
  transform: translateX(0);
}
.slide-leave-from {
  transform: translateX(0);
}
.slide-leave-to {
  transform: translateX(-100%);
}
.slide-enter-active,
.slide-leave-active {
  transition: transform 0.3s ease;
}
</style>
