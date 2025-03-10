<template>
    <header>
        <h1>{{title}}</h1>
    </header>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    title: String
})
</script>
