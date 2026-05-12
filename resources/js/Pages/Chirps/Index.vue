<script setup>
import MyLayout from '@/Layouts/MyLayout.vue';
    defineProps(['title', 'subtitle'])
</script>

<template>
    <MyLayout>
        <template #title>
            <h1>{{ title }}</h1>
        </template>
        <h2>{{ subtitle }}</h2>
    </MyLayout>
</template>
