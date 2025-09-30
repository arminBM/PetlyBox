<script setup>
import { ref, onMounted, onUnmounted, nextTick } from "vue"

const showPopup = ref(false)
const emailOrPhone = ref("")

const emit = defineEmits(["closed"])

onMounted(async () => {
  setTimeout(async () => {
    showPopup.value = true
    await nextTick()
    const el = document.getElementById("popup-contact")
    el?.focus()
  }, 800)

  
  window.addEventListener("keydown", onEsc)
})

onUnmounted(() => {
  window.removeEventListener("keydown", onEsc)
})

function onEsc(e) {
  if (e.key === "Escape") closePopup()
}

function closePopup() {
  if (!showPopup.value) return
  showPopup.value = false
  emit("closed") 
}

function register() {
  if (!emailOrPhone.value) return
  alert(`Registered: ${emailOrPhone.value}`)
  closePopup() 
}

function onBackdropClick(e) {
  if (e.target === e.currentTarget) closePopup()
}
</script>

<template>
  <transition name="fade">
    <div
      v-if="showPopup"
      class="fixed inset-0 bg-black/50 flex items-center justify-center z-50"
      @click="onBackdropClick"
      role="dialog"
      aria-modal="true"
      aria-labelledby="popup-title"
    >
      <transition name="scale">
        <div v-if="showPopup" class="bg-white rounded-2xl shadow-2xl w-96 max-w-[92vw] p-6 relative">
          <button
            @click="closePopup"
            class="absolute top-3 right-3 text-gray-500 hover:text-gray-800 transition"
            aria-label="Close"
          >
            ✖
          </button>

          <h2 id="popup-title" class="text-2xl font-bold text-center mb-2 text-gray-800">
            🎉 Special Offer!
          </h2>
          <p class="text-center text-gray-600 mb-4">
            First-time visitors get <span class="font-semibold">20% OFF</span> their first PetlyBox.
          </p>

          <input
            id="popup-contact"
            v-model="emailOrPhone"
            type="text"
            placeholder="Enter your email or phone"
            class="w-full border border-gray-300 rounded-lg px-4 py-2 mb-4 focus:outline-none focus:ring-2 focus:ring-yellow-400"
          />

          <button
            @click="register"
            class="w-full bg-yellow-500 hover:bg-yellow-600 text-black font-semibold py-2 rounded-lg transition"
          >
            Register Now
          </button>
        </div>
      </transition>
    </div>
  </transition>
</template>

<style>
.fade-enter-active,
.fade-leave-active { transition: opacity 0.3s ease; }
.fade-enter-from,
.fade-leave-to { opacity: 0; }

.scale-enter-active,
.scale-leave-active { transition: transform 0.3s ease, opacity 0.3s ease; }
.scale-enter-from,
.scale-leave-to { transform: scale(0.8); opacity: 0; }
</style>
