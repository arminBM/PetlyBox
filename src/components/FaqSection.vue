<script setup>
import { ref } from 'vue'
import FaqItemOverlay from './FaqItemOverlay.vue'

const faqs = [
  { q: 'How long does shipping take?', a: 'Your first PetlyBox ships within 5 days. After that, boxes arrive around the same time each month.' },
  { q: 'Can I cancel anytime?', a: 'Yes! Pause or cancel anytime from your account dashboard.' },
  { q: 'What about allergies?', a: 'We offer allergy-friendly options. Tell us at checkout or in your account.' },
  { q: 'Do you ship internationally?', a: 'We currently ship within the US; international shipping is coming soon.' },
]

const openIndex = ref(-1)
const isOpen = (i) => openIndex.value === i
const setOpen = (i) => { openIndex.value = isOpen(i) ? -1 : i }
</script>

<template>
  <section class="py-16 bg-white pb-24">
    <div class="mx-auto max-w-4xl px-4">
      <h2 class="text-3xl font-semibold text-center mb-8">Frequently Asked Questions</h2>

      <!-- No divide-y: give each row its own border so no line shows behind the overlay -->
      <div>
        <FaqItemOverlay
          v-for="(faq, i) in faqs"
          :key="i"
          :q="faq.q"
          :a="faq.a"
          :id="`faq-${i}`"
          :model-value="isOpen(i)"
          @update:modelValue="setOpen(i)"
          class="border-b border-gray-200"
        />
      </div>
    </div>
  </section>
</template>
