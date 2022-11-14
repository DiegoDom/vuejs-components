<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      type="button"
      class="btn btn-outline-primary"
      @click="emit('prev')"
      :disabled="inicio <= 0"
    >
      Anterior
    </button>
    <button
      type="button"
      class="btn btn-outline-primary"
      :disabled="fin >= total"
      @click="emit('next')"
    >
      Siguiente
    </button>
  </div>
</template>

<script setup>
defineProps({
  inicio: {
    required: true,
    default: 0,
    type: Number,
  },
  fin: {
    required: true,
    default: 10,
    type: Number,
  },
  total: {
    required: true,
    default: 0,
    type: Number,
  },
});
const emit = defineEmits(['next', 'prev']);
</script>
