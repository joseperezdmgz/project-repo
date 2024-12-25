<template>
    <li class="border p-2 mb-2 flex flex-col gap-4">
        <h3 class="text-lg font-bold">{{ details.productName }}</h3>
        <p class="text-gray-600 mb-2">
            <span class="font-medium">Type: </span>
            <span>{{ details.productTypeName.toUpperCase() }}</span>
        </p>
        <p class="text-gray-600 mb-2">
            <span class="font-medium">Speed: </span>
            <span>{{ details.mbSpeed }} Mbps</span>
        </p>

        <p class="text-gray-600 mb-2">
            <span class="font-medium">Data: </span>
            <span>{{ details.gbData ? `${details.gbData} GB` : 'N/A' }}</span>
        </p>

        <p class="text-gray-600 mb-2">
            <span class="font-medium">Terminal Number: </span>
            <span>{{ details.numeracioTerminal }}</span>
        </p>

        <p class="text-gray-600 mb-2">
            <span class="font-medium">Sale Date: </span>
            <span>{{ formatDate(details.soldAt) }}</span>
        </p>
    </li>
</template>

<script setup>
    const props = defineProps ({
        details: {
            type: Object,
            required: true,
        }
    })

    const formatDate = (dateString) => {
    const date = new Date(dateString);
    const day = String(date.getDate()).padStart(2, '0');
    const month = String(date.getMonth() + 1).padStart(2, '0');
    const year = date.getFullYear();
    const hours = String(date.getHours()).padStart(2, '0');
    const minutes = String(date.getMinutes()).padStart(2, '0');
    return `${day}/${month}/${year} ${hours}:${minutes}`;
    }
</script>