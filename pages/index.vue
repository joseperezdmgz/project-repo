<template>
    <p>Prueba</p>
    <pre>
        {{ customers }}
    </pre>
</template>

<script setup>


const apiUrl = useRuntimeConfig().public.apiUrl;
  const searchQuery = ref('');
  const sort = ref('id');

  const { data: customers } = await useAsyncData(() =>
    $fetch(`${apiUrl}customers?_sort=${sort})`)
  );

    useHead({
        title: 'Prueba'
    });
</script>