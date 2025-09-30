<script setup>
const props = defineProps({
  title: { type: String, required: true },
  price: { type: Number, required: true },
  perks: { type: Array, default: () => [] },
  popular: { type: Boolean, default: false }
})
</script>

<template>
  <div
    :class="[
      'flex flex-col justify-between rounded-2xl shadow-lg p-6 bg-white text-center transition-transform hover:scale-105',
      popular ? 'ring-2 ring-yellow-500' : ''
    ]"
  >
   
    <div v-if="popular" class="mb-2">
      <span class="inline-block bg-yellow-500 text-black text-xs font-semibold px-3 py-1 rounded-full">
        Most Popular
      </span>
    </div>

    <h3 class="text-xl font-semibold mb-2">{{ title }}</h3>
    <p class="text-4xl font-bold mb-4">
      ${{ price }}<span class="text-base font-medium">/mo</span>
    </p>

    <ul class="text-left space-y-2 mb-6">
      <li v-for="(perk, i) in perks" :key="i" class="flex items-start">
        <span class="mr-2 text-yellow-500">✔</span>
        <span>{{ perk }}</span>
      </li>
    </ul>

    <button
      class="bg-yellow-500 hover:bg-yellow-600 text-black font-semibold py-2 px-6 rounded-full focus:outline-none focus:ring-2 focus:ring-yellow-400"
    >
      Choose plan
    </button>
  </div>
</template>
