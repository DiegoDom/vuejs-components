<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>App</h1>
    <h2>Mi post favorito: {{ favorito?.title }}</h2>
    <PaginatePost @next="next" @prev="prev" :inicio="inicio" :fin="fin" :total="posts.length" />
    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :id="post.id"
      :title="post.title"
      :body="post.body"
      :favorito_id="favorito?.id || undefined"
      @setFavorito="cambiarFavorito"
    />
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([]);
const loading = ref(true);

const postPorPagina = 10;
const inicio = ref(0);
const fin = ref(postPorPagina);

const favorito = ref();

const cambiarFavorito = (post) => (favorito.value = post);

const next = () => {
  if (fin.value >= posts.value.length) return;
  inicio.value += postPorPagina;
  fin.value += postPorPagina;
};

const prev = () => {
  if (inicio.value <= 0) return;
  inicio.value -= postPorPagina;
  fin.value -= postPorPagina;
};

onMounted(async () => {
  try {
    const resp = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await resp.json();
  } catch (error) {
    console.log(error);
    posts.value = [];
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 1500);
  }
});

/* fetch('https://jsonplaceholder.typicode.com/posts')
  .then((resp) => resp.json())
  .then((data) => (posts.value = data))
  .catch((e) => {
    console.log(e);
    posts.value = [];
  })
  .finally(() => (loading.value = false)); */
</script>
