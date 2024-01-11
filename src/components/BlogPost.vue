<script setup>
//defineProps(['title', 'body', 'id', 'colorText']);

defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: "Sin descripcion"
    }
});

const emit = defineEmits(['changeFavorite'])

</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 
                class="card-title" 
            >
               {{ id }} – {{ title }}
            </h5>
            <p>{{ body }}</p>
            <button class="btn btn-outline-primary" @click="emit('changeFavorite', title)">Favorito</button>
        </div>
    </div>
</template>