<script setup>
    //defineProps(['title', 'id', 'description'])
    defineProps({
        title: String,
        id: Number,
        body:{
            type: String,
            default: 'Sin description para mostrar'
        }
    })
</script>

<template>

    <div class="card mt-2 mb-3">
        <div class="card-body">
          <h5>{{ id }} - {{ title }}</h5>
          <p>{{ body }}</p>
          <button @click="$emit('addfavorito', title)" class="btn btn-sm btn-outline-warning">agregar a favorito</button>
        </div>
    </div>

</template>