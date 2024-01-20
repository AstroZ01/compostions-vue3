<script setup>
//defineProps(['title',"id",'body'])
defineProps ({
    title: String,
    id: Number,
    body: {
        type: String,
        default:'sin descripcion',
    },
    cambiarFavorito: Function
});


const emit = defineEmits (['cambiarFavoritoNombre'])
//emit
</script>
<template>
<div class="card">
    <div class="card-body">
        <h5 class="card-tittle">{{ id }} - {{title}}</h5>
        <p>{{body}}</p>
        <button @click="cambiarFavorito(title)" 
        class="btn btn-outline-primary">Favorito</button>
    </div>
</div>
</template>