<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import { Head, useForm, usePage } from '@inertiajs/vue3';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputError from '@/Components/InputError.vue';
import CrudItem from '@/Components/CrudItem.vue';

const form = useForm({
    name: '',
    description: '',
});

function submit() {
    form.post(route('cruds.store'), {
        onSuccess: () => form.reset(),
        preserveState: false,
    })
}

defineProps([
    'cruds',
]);
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
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 mt-6">
                <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="px-6 py-4 border-b border-gray-200 dark:border-gray-700 flex items-center justify-between">
                        <h3 class="text-lg font-semibold text-gray-800 dark:text-gray-200">
                            Listado de Cruds
                        </h3>
                        <span class="inline-flex items-center px-3 py-1 text-xs font-medium text-emerald-700 bg-emerald-100 rounded-full dark:bg-emerald-900/40 dark:text-emerald-300">
                            {{ cruds.length }} {{ cruds.length === 1 ? 'registro' : 'registros' }}
                        </span>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="min-w-full divide-y divide-gray-200 dark:divide-gray-700">
                            <thead class="bg-gray-50 dark:bg-gray-900/50">
                                <tr>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                        ID
                                    </th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                        Nombre
                                    </th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                        Descripción
                                    </th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                        Creado
                                    </th>
                                    <th scope="col" class="px-6 py-3 text-right text-xs font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider">
                                        Acciones
                                    </th>
                                </tr>
                            </thead>
                            <tbody class="bg-white dark:bg-gray-800">
                                <CrudItem v-for="crud in cruds" :key="`crud-${crud.id}`" :crud="crud" />
                                <tr v-if="cruds.length === 0">
                                    <td colspan="5" class="px-6 py-12 text-center text-sm text-gray-500 dark:text-gray-400">
                                        No hay registros disponibles.
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
