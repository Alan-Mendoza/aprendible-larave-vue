<script setup>
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputError from '@/Components/InputError.vue';
import AppLayout from '@/Layouts/AppLayout.vue';
import { Head } from '@inertiajs/vue3';
import axios from 'axios';
import { ref } from 'vue';

const message = ref('');
const errors = ref({});
const processing = ref(false);

function submit() {
    processing.value = true;
    axios.post(route('chirps.store'), { message: message.value })
        .then((res) => {
            console.log(res.data);
            message.value = '';
            errors.value = {};
        }).catch((error) => {
            // console.log(error.response.status)
            if (error.response.status === 422) {
                errors.value = error.response.data.errors;
                return; // Salir de la función para evitar mostrar el mensaje de error genérico
            }
            // console.log(error.response.data.errors);
            // errors.value = error.response.data.errors;
            console.error(error.response.data.message); // Super importante para ver el mensaje de error específico en la consola
        }).finally(() => {
            processing.value = false;
        });
}

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
                    <form @submit.prevent="submit">
                        <textarea v-model="message" placeholder="Que estas pensando ?" class="block w-full rounded-md border-gray-300 dark:border-gray-600 dark:bg-gray-700 dark:text-gray-300 focus:border-emerald-500 focus:ring-emerald-500"></textarea>
                        <!-- <div v-if="errors.message" class="text-red-500 text-sm mt-1">
                            {{ errors.message && errors.message[0] }}
                        </div> -->
                        <InputError :message="errors.message && errors.message[0]" class="mt-2" />
                        <PrimaryButton :disabled="processing">
                            {{ processing ? 'Enviando...' : 'Chirps' }}
                        </PrimaryButton>
                    </form>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
