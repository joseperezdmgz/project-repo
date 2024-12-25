<template>
    <ul v-if="details" class="w-full border mt-10 rounded">
        <li class="p-6 flex justify-between">
            <h3 class="text-xl font-700">{{ details.givenName }}</h3>
            <p>{{ details.id }}</p>
        </li>
        <hr>
        <li class="p-6 grid grid-cols-2 gap-4 border-b">
            <p class="text-sm font-medium text-gray-500">
                Full name
            </p>
            <p class="text-sm font-medium">
                {{ details.givenName }} {{ details.familyName1 }}
            </p>
        </li>
        <li class="p-6 grid grid-cols-2 gap-4 border-b">
            <p class="text-sm font-medium text-gray-500">
                Email
            </p>
            <p class="text-sm font-medium">
                {{ details.email }}
            </p>
        </li>
        <li class="p-6 grid grid-cols-2 gap-4 border-b">
            <p class="text-sm font-medium text-gray-500">
                Phone
            </p>
            <p class="text-sm font-medium">
                {{ details.phone }}
            </p>
        </li>
        <li class="p-6 grid grid-cols-2 gap-4 border-b">
            <p class="text-sm font-medium text-gray-500">
                {{ details.docType.toUpperCase() }}
            </p>
            <p class="text-sm font-medium">
                {{ details.docNum }}
            </p>
        </li>
    </ul>
</template>

<script setup>
const props = defineProps ({
    details: {
        type: Object,
    }
})
</script>
