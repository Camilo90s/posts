<script setup>
// defineProps(['title', 'id', 'body']);

defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: 'Sin descripcion',
    }
});

const emit = defineEmits(['cambiarFavorito']);
</script>

<template>
    <article class="flex flex-col rounded-lg bg-white shadow-sm ring-1 ring-gray-200 transition hover:shadow-md hover:ring-gray-300">
        <div class="flex flex-1 flex-col gap-2 p-4 sm:p-6">
            <span class="text-xs font-medium text-green-500">Post #{{ id }}</span>
            <h5 class="text-base font-semibold text-gray-900 first-letter:uppercase">{{ title }}</h5>
            <p class="line-clamp-3 text-sm leading-6 text-gray-500">{{ body }}</p>
        </div>

        <div class="border-t border-gray-200 px-4 py-3 sm:px-6">
            <button class="inline-flex items-center rounded-md bg-green-500 px-2.5 py-1.5 text-sm font-medium text-white shadow-sm transition-colors hover:bg-green-600 focus:outline-none focus-visible:ring-2 focus-visible:ring-green-500 focus-visible:ring-offset-2"
            @click="emit('cambiarFavorito', title)">Favorito</button>
        </div>
    </article>
</template>