<script setup>
import { computed } from 'vue'

const props = defineProps({
  visible: { type: Boolean, default: false },
  shape: { type: String, default: 'circle' },
  text: { type: String, default: '🎉 20% OFF your first PetlyBox!' }
})
const emit = defineEmits(['update:visible', 'click'])

const show = computed({
  get: () => props.visible,
  set: v => emit('update:visible', v)
})

const shapeClass = computed(() =>
  props.shape === 'square' ? 'rounded-2xl' : 'rounded-full'
)
</script>

<template>
  <transition name="slide-left">
    <div
      v-if="show"
      class="fixed bottom-6 left-6 z-[60] select-none"
      role="status" aria-live="polite"
    >
      <div
        :class="[
          'flex items-center gap-3 shadow-lg ring-1 ring-black/10 bg-yellow-400 text-black',
          'px-4 py-3',
          'w-auto max-w-[90vw] sm:max-w-xs',
          shapeClass
        ]"
      >
        <button
          class="shrink-0 w-10 h-10 flex items-center justify-center rounded-full bg-black/10 hover:bg-black/20 focus:outline-none focus-visible:ring-2 focus-visible:ring-black/40"
          @click="$emit('click')"
          aria-label="Open promotion"
          title="Open promotion"
        >💛</button>

        <p class="text-sm font-medium leading-snug pr-2">
          {{ text }}
        </p>

        <button
          @click="show = false"
          class="ml-auto text-black/70 hover:text-black focus:outline-none focus-visible:ring-2 focus-visible:ring-black/40 rounded"
          aria-label="Close announcement"
          title="Close"
        >✕</button>
      </div>
    </div>
  </transition>
</template>

<style scoped>

.slide-left-enter-from,
.slide-left-leave-to { opacity: 0; transform: translateX(-16px); }
.slide-left-enter-to,
.slide-left-leave-from { opacity: 1; transform: translateX(0); }
.slide-left-enter-active,
.slide-left-leave-active { transition: transform .25s ease, opacity .25s ease; }

@media (prefers-reduced-motion: reduce) {
  .slide-left-enter-active, .slide-left-leave-active { transition: none; }
}
</style>
