<script setup>
defineProps(["inicio", "fin","maxLength"]);

const emit = defineEmits (['next','prev']);

const activarSiguiente = () => {
  console.log('me diste siguiente')
  emit('next');
}
</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
  <button type="button"
   class="btn btn-secondary"
    @click="$emit('prev')"
    :disabled="inicio === 0">Previus {{ inicio }}</button>
  <button type="button" 
  class="btn btn-secondary"
   @click="$emit('next')" :disabled="fin >= maxLength">Next {{ fin }}</button>
</div>
</template>