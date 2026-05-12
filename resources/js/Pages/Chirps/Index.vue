<script setup>
    const title = 'Title from Vue';
    defineProps(['subtitle'])
</script>

<template>
    <h1>{{ title }}</h1>
    <h2>{{ subtitle }}</h2>
</template>
