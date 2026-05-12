<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputError from '@/Components/InputError.vue';

const form = useForm({
    name: '',
    description: '',
});

function submit() {
    form.post(route('cruds.store'), {
        onSuccess: () => form.reset(),
    })
}
</script>

<template>
    <AppLayout>
        <Head title="Crud">
            <meta name="description" content="Crud description" />
        </Head>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">
                Crud
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-gray-800 dark:text-gray-200 p-5 overflow-hidden shadow-xl sm:rounded-lg">
                    <form @submit.prevent="submit">
                        <input v-model="form.name" placeholder="Nombre" class="block w-full rounded-md border-gray-300 dark:border-gray-600 dark:bg-gray-700 dark:text-gray-300 focus:border-emerald-500 focus:ring-emerald-500"></input>
                        <InputError :message="form.errors.name" class="mt-2" />

                        <input v-model="form.description" placeholder="Descripción" class="block w-full rounded-md border-gray-300 dark:border-gray-600 dark:bg-gray-700 dark:text-gray-300 focus:border-emerald-500 focus:ring-emerald-500 mt-4"></input>
                        <InputError :message="form.errors.description" class="mt-2" />
                        <PrimaryButton :disabled="form.processing">
                            {{ form.processing ? 'Enviando...' : 'Chirps' }}
                        </PrimaryButton>
                    </form>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
