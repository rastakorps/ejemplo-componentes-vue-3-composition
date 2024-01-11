<script setup>

defineProps([ 'start', 'end', 'maxLength']);
const emit = defineEmits(['nextPage', 'previousPage']);
</script>

<template>
    <div class="btn-group">
        <button 
            type="button" 
            class="btn btn-outline-primary"
            @click="emit('previousPage')"
            :disabled="start <= 0"
        >
            previous
        </button>
        <button 
            type="button" 
            class="btn btn-outline-primary"
            @click="emit('nextPage')"
            :disabled="end >= maxLength"
        >
            Next
        </button>
    </div>
</template>