<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  q: { type: String, required: true },
  a: { type: String, required: true },
  modelValue: { type: Boolean, default: false },
  id: { type: String, default: '' }
})
const emit = defineEmits(['update:modelValue'])

const root = ref(null)
const close = () => emit('update:modelValue', false)
const toggle = () => emit('update:modelValue', !props.modelValue)

function onKeydown(e) { if (e.key === 'Escape') close() }
function onDocClick(e) {
  if (!props.modelValue) return
  const el = root.value
  if (el && !el.contains(e.target)) close()
}

onMounted(() => {
  document.addEventListener('keydown', onKeydown)
  document.addEventListener('click', onDocClick, true)
})
onUnmounted(() => {
  document.removeEventListener('keydown', onKeydown)
  document.removeEventListener('click', onDocClick, true)
})
</script>

<template>
  <div ref="root" class="relative py-2">
    <button
      @click="toggle"
      :aria-expanded="modelValue.toString()"
      :aria-controls="(id || q).replace(/\s+/g,'-') + '-panel'"
      class="w-full flex items-center justify-between gap-4 py-4 text-left font-medium
             focus:outline-none focus-visible:ring-2 focus-visible:ring-yellow-400"
    >
      <span class="text-lg text-black">{{ q }}</span>
      <svg
        class="h-5 w-5 shrink-0 transition-transform duration-200"
        :class="modelValue ? 'rotate-180' : ''"
        viewBox="0 0 20 20" fill="currentColor" aria-hidden="true"
      >
        <path
          fill-rule="evenodd"
          d="M5.23 7.21a.75.75 0 011.06.02L10 10.17l3.71-2.94a.75.75 0 111.04 1.08l-4.24 3.36a.75.75 0 01-.94 0L5.21 8.31a.75.75 0 01.02-1.1z"
          clip-rule="evenodd"
        />
      </svg>
    </button>

    <transition name="fade-ans">
      <div
        v-if="modelValue"
        :id="(id || q).replace(/\s+/g,'-') + '-panel'"
        role="region"
        class="absolute left-0 right-0 top-full mt-2 z-20
               rounded-xl bg-white shadow-xl ring-1 ring-black/10
               p-4 text-slate-700"
      >
        {{ a }}
      </div>
    </transition>
  </div>
</template>

<style scoped>
.fade-ans-enter-from,
.fade-ans-leave-to { opacity: 0; transform: translateY(-4px) scale(0.98); }
.fade-ans-enter-to,
.fade-ans-leave-from { opacity: 1; transform: translateY(0) scale(1); }
.fade-ans-enter-active,
.fade-ans-leave-active { transition: opacity .24s ease, transform .24s ease; }

button:focus:not(:focus-visible) { outline: none; box-shadow: none; }

@media (prefers-reduced-motion: reduce) {
  .fade-ans-enter-active, .fade-ans-leave-active { transition: none; }
}
</style>
