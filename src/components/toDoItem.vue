<script setup>

    import { defineProps } from 'vue';

    defineProps({
        id:          String,
        description: String,
        completed:   Boolean
    });

</script>



<template>

    <a class="list-group-item list-group-item-action" :class="completed ? 'list-group-item-success' : ''">
        <input class="form-check-input me-3" type="checkbox" :checked="completed" @click="completed = !completed">
        <span> {{ id }} - {{ description }} - {{ completed ? 'Completed' : 'Non completed' }} </span>
    </a>

</template>
