<script setup>
    defineProps({
        crud: Object,
    });
</script>

<template>
    <tr class="border-b border-gray-200 dark:border-gray-700 hover:bg-emerald-50 dark:hover:bg-gray-700/50 transition-colors">
        <td class="px-6 py-4 text-sm font-medium text-gray-900 dark:text-gray-100">
            #{{ crud.id }}
        </td>
        <td class="px-6 py-4 text-sm font-semibold text-gray-900 dark:text-gray-100">
            {{ crud.name }}
        </td>
        <td class="px-6 py-4 text-sm text-gray-600 dark:text-gray-300 max-w-md">
            <span class="line-clamp-2">{{ crud.description || '—' }}</span>
        </td>
        <td class="px-6 py-4 text-sm text-gray-500 dark:text-gray-400 whitespace-nowrap">
            {{ new Date(crud.created_at).toLocaleDateString() }}
        </td>
        <td class="px-6 py-4 text-right text-sm">
            <div class="flex justify-end gap-2">
                <button class="inline-flex items-center px-3 py-1.5 text-xs font-semibold text-emerald-700 bg-emerald-100 rounded-md hover:bg-emerald-200 dark:bg-emerald-900/40 dark:text-emerald-300 dark:hover:bg-emerald-900/60 transition-colors">
                    Editar
                </button>
                <button class="inline-flex items-center px-3 py-1.5 text-xs font-semibold text-red-700 bg-red-100 rounded-md hover:bg-red-200 dark:bg-red-900/40 dark:text-red-300 dark:hover:bg-red-900/60 transition-colors">
                    Eliminar
                </button>
            </div>
        </td>
    </tr>
</template>
