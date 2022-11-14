<template>
  <div class="card my-2">
    <div class="card-body">
      <h5 class="card-title">{{ id }}.- {{ title }}</h5>
      <p>{{ body }}</p>
      <button
        @click="onChangeFavorito({ id, title })"
        :class="`btn btn-sm ${favorito_id === id ? 'btn-primary' : 'btn-outline-primary'} `"
      >
        Favorito
      </button>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  favorito_id: {
    type: Number,
    default: 0,
  },
  id: {
    required: true,
    type: Number,
  },
  title: {
    required: true,
    type: String,
  },
  body: {
    type: String,
    default: 'POST SIN CUERPO',
  },
});

const emit = defineEmits(['setFavorito']);

const onChangeFavorito = (post) =>
  post.id === props.favorito_id ? emit('setFavorito', undefined) : emit('setFavorito', post);
</script>
