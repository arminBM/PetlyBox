<script setup>
import PriceCard from './PriceCard.vue'

const plans = [
  {
    title: 'Monthly',
    price: 29,
    perks: ['2 toys + 2 treats + surprise', 'Free shipping over $40', 'Cancel anytime'],
    popular: false
  },
  {
    title: 'Quarterly',
    price: 79,
    perks: ['Save $8', '2 toys + 2 treats + surprise', 'Free shipping over $40'],
    popular: true
  },
  {
    title: 'Annual',
    price: 299,
    perks: ['Save $49', '2 toys + 2 treats + surprise', 'Free shipping over $40'],
    popular: false
  }
]
</script>

<template>
  <section class="py-16 bg-gray-50">
    <div class="mx-auto max-w-6xl px-4 text-center">
      <h2 class="text-3xl font-semibold mb-10">Choose Your Plan</h2>
      <div class="grid gap-8 md:grid-cols-3">
        <PriceCard
          v-for="plan in plans"
          :key="plan.title"
          :title="plan.title"
          :price="plan.price"
          :perks="plan.perks"
          :popular="plan.popular"
        />
      </div>
    </div>
  </section>
</template>
