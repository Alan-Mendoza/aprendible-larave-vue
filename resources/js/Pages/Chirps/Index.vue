<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import { Head, Link } from '@inertiajs/vue3';

defineProps(['title', 'subtitle']);
</script>

<template>
    <AppLayout>
        <Head title="Chirps">
            <meta name="description" content="Chirps description" />
        </Head>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">
                {{ title }}
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-gray-800 dark:text-gray-200 overflow-hidden shadow-xl sm:rounded-lg p-5">
                    <Link :href="route('dashboard')">Dashboard</Link>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
