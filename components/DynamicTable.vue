<template>
    <div class="relative overflow-auto shadow-md sm:rounded-lg">
        <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
            <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                <tr>
                    <template v-for="column in props.columns" :key="column.name">
                        <th 
                            v-if="column.visible" 
                            scope="col" 
                            class="px-6 py-3 cursor-pointer"
                            @click="sortBy(column.value)"
                        >
                            {{ column.name }}
                            <span v-if="sort.column === column.value">
                                {{ sort.direction === 'asc' ? '▲' : '▼' }}
                            </span>
                        </th>
                    </template>
                    <th v-if="link" scope="col" class="px-6 py-3">
                        Acciones
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr 
                    v-for="row in sortedRows" 
                    :key="row.id" 
                    class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b dark:border-gray-700"
                >
                    <template v-for="column in props.columns" :key="column.value">
                        <td v-if="column.visible" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            {{ row[column.value] }}
                        </td>
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
            required: true,
        },
        rows: {
            type: Array,
            required: true,
        },
        link: {
            type: String,
            required: false,
            default: '',
        },
    });

    // Estado de ordenación
    const sort = ref({
        column: '', 
        direction: 'asc',
    });

    // Computed para ordenar las filas
    const sortedRows = computed(() => {
        if (!sort.value.column) return props.rows; // Si no hay columna seleccionada, devuelve todas las filas

        // Ordenar las filas según la columna y la dirección
        const sorted = [...props.rows].sort((a, b) => {
            const aValue = a[sort.value.column];
            const bValue = b[sort.value.column];

            if (aValue < bValue) return sort.value.direction === 'asc' ? -1 : 1;
            if (aValue > bValue) return sort.value.direction === 'asc' ? 1 : -1;
            return 0;
        });

        return sorted;
    });

    // Función para cambiar el orden cuando se hace clic en el encabezado de la columna
    const sortBy = (column) => {
        if (sort.value.column === column) {
            // Si la columna ya está ordenada, cambia la dirección
            sort.value.direction = sort.value.direction === 'asc' ? 'desc' : 'asc';
        } else {
            // Si es una columna diferente, establece la dirección ascendente por defecto
            sort.value.column = column;
            sort.value.direction = 'asc';
        }
    };
</script>