<template>
    <div class="relative overflow-auto shadow-md sm:rounded-lg">
        <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
            <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                <tr>
                    <template v-for="column in props.columns">
                        <th v-if="column.visible" :key="column.name" scope="col" class="px-6 py-3">
                            {{ column.name }}
                        </th>
                    </template>
                    <th v-if="link" scope="col" class="px-6 py-3">
                        Acciones
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="row in props.rows" :key="row.id" class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b dark:border-gray-700">
                    <template v-for="column in props.columns">
                        <th v-if="column.visible" :key="column.value" scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white" >
                            {{row[column.value] }}
                        </th>
                    </template>
                    <td v-if="link" class="px-6 py-4">
                        <NuxtLink :to="`${props.link}/${row.customerId}`" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Ver</NuxtLink>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
    const props = defineProps({
        columns: {
        type: Array,
        required: true
        },
        rows: {
        type: Array,
        required: true
        },
        link: {
        type: String,
        required: false,
        default: ""
        }
    });
</script>