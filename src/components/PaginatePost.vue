<script setup>
defineProps(['inicio', 'fin', 'maxLength']);
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button @click="$emit('prev')" type="button" class="btn btn-outline-primary" :disabled="inicio === 0">Anterior</button>
        <button @click="$emit('next')" type="button" class="btn btn-outline-primary" :disabled="fin >= maxLength">Siguiente</button>
    </div>
</template>