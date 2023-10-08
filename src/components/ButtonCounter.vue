<script setup>
import { ref } from 'vue'
let contador = ref(0);
const aumentar = ()=> contador.value++;
</script>

<template>
<button class="btn btn-success" @click="aumentar()">Counter {{ contador }}</button>
</template>