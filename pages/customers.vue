<template>
  <input v-model="searchQuery" type="text" placeholder="Buscar cliente..." class="mb-4 p-2 border w-full" />
  <DynamicTable :columns="columns" :rows="customers" link="/customer"/>
</template>
  
<script setup>
  const columns = ref([
    { name: 'ID', value: 'id', visible: true },
    { name: 'docType', value: 'docType', visible: false },
    { name: 'DNI/NIF/CIF', value: 'docNum', visible: true },
    { name: 'email', value: 'email', visible: true },
    { name: 'customerId', value: 'customerId', visible: false },
    { name: 'name', value: 'givenName', visible: true },
    { name: 'surname', value: 'familyName1', visible: true },
    { name: 'phone', value: 'phone', visible: true },
  ]);
  const apiUrl = useRuntimeConfig().public.apiUrl;
  const searchQuery = ref('');
  const sort = ref('id');

  const { data: customers } = await useAsyncData(() =>
    $fetch(`${apiUrl}customers?_sort=id`)
  );

  // Computed para filtrar los customers basados en la búsqueda
  const filteredcustomers = computed(() => {
    if (!searchQuery.value) return customers.value; // Si no hay búsqueda, devolver todos los customers

    const lowerSearchQuery = searchQuery.value.toLowerCase();
    return customers.value.filter(post => 
      post.title.toLowerCase().includes(lowerSearchQuery) || 
      post.body.toLowerCase().includes(lowerSearchQuery)
    );
  });
// SEO
  useHead({
    title: 'Customers'
  })
</script>