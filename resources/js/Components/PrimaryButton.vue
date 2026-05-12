<script setup>
defineProps({
    type: {
        type: String,
        default: 'submit',
    },
});
</script>

<template>
    <button :type="type" class="mt-2 bg-emerald-500 hover:bg-emerald-700 text-white font-bold py-2 px-4 rounded dark:bg-emerald-500 dark:hover:bg-emerald-800">
        <slot />
    </button>
</template>
