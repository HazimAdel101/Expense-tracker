<template>
    <h4>Your balance </h4>
    <h1>${{ total }}</h1>
</template>

<script setup>
import { defineProps } from 'vue';

    const props = defineProps({
        total: Number,
        required: true,
    })

</script>