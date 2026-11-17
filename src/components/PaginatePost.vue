<script setup>
const emit = defineEmits(['next', 'prev']);

defineProps({
  inicio: Number,
  fin: Number,
  maxLength: Number
})
</script>

<template>
    <nav class="my-8 flex items-center justify-end gap-2 pt-6" aria-label="Paginación">

    <button class="inline-flex items-center gap-1.5 rounded-md bg-white px-2.5 py-1.5 text-sm font-medium text-gray-700 shadow-sm ring-1 ring-inset ring-gray-300 transition-colors hover:bg-gray-50 focus:outline-none focus-visible:ring-2 focus-visible:ring-green-500 disabled:pointer-events-none disabled:opacity-50" @click="emit('prev')" :disabled="inicio === 0">
      <svg viewBox="0 0 24 24" class="size-4" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="m15 18-6-6 6-6" />
      </svg>
      Previus
    </button>

    <button class="inline-flex items-center gap-1.5 rounded-md bg-green-500 px-2.5 py-1.5 text-sm font-medium text-white shadow-sm transition-colors hover:bg-green-600 focus:outline-none focus-visible:ring-2 focus-visible:ring-green-500 focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50" @click="emit('next')" :disabled="fin >= maxLength">
      Next
      <svg viewBox="0 0 24 24" class="size-4" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="m9 18 6-6-6-6" />
      </svg>
    </button>

  </nav>
</template>