<script setup>
import { onMounted, ref } from 'vue'

import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([]);
const postXpage = 9;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const favorito = ref('');

const cambiarFavorito = (title) => {
  favorito.value = title;
};

const next = () => {
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
};

const prev = () => {
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage;
};

const url = 'https://jsonplaceholder.typicode.com/posts';

// onMounted(async () => {
//   try {
//     const res = await fetch(url);
//     posts.value = await res.json();
//   } catch (error) {
//     console.log(error);
//   } finally {
//     loading.value = false;
//   }
// });


// fetch(url)
//   .then(res => res.json())
//   .then(data => posts.value = data)
//   .finally(() => loading.value = false)

const fetchData = async () => {
  try {
    const res = await fetch(url);
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false;
  }
};

fetchData();

</script>

<template>
  <div class="min-h-screen bg-white text-gray-900 antialiased">

    <header class="sticky top-0 z-10 border-b border-gray-200 bg-white/75 backdrop-blur">
      <div class="mx-auto flex h-16 max-w-7xl items-center justify-between px-4 sm:px-6 lg:px-8">
        <h1 class="text-xl font-bold tracking-tight">App</h1>

        <span class="inline-flex items-center rounded-md bg-green-50 px-2 py-1 text-xs font-medium text-green-600 ring-1 ring-inset ring-green-500/25">
          {{ posts.length }} posts
        </span>
      </div>
    </header>

    <LoadingSpinner v-if="loading"></LoadingSpinner>

    <main class="mx-auto max-w-7xl px-4 py-8 sm:px-6 lg:px-8" v-else>

      <div class="mb-8 rounded-lg bg-gray-50 p-4 ring-1 ring-gray-200">
        <h2 class="text-sm font-medium text-gray-500">Mi post favorito</h2>
        <p class="mt-1 font-semibold text-gray-900 first-letter:uppercase">
          {{ favorito || 'Aún no has elegido ninguno' }}
        </p>
      </div>

      <PaginatePost
      :inicio="inicio"
      :fin="fin"
      :maxLength="posts.length"
      @next="next"
      @prev="prev"></PaginatePost>

      <div class="grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <BlogPost 
          v-for="post in posts.slice(inicio, fin)"
          :key="post.id"
          :title="post.title"
          :id="post.id"
          :body="post.body"
          @cambiarFavorito = 'cambiarFavorito'
        ></BlogPost>
      </div>
    </main>
  </div>
</template>