<template>
  <div>
    <input v-model="searchQuery" type="text" placeholder="Buscar cliente..." class="mb-4 p-2 border w-full" />

    <DynamicTable 
      :columns="columns" 
      :rows="sortedFilteredCustomers" 
      link="/customer"
      @sort="handleSort"
    />
  </div>
</template>

<script setup>
  const columns = ref([
    { name: 'ID', value: 'id', visible: true },
    { name: 'DNI/NIF/CIF', value: 'docNum', visible: true },
    { name: 'Email', value: 'email', visible: true },
    { name: 'Name', value: 'givenName', visible: true },
    { name: 'Surname', value: 'familyName1', visible: true },
    { name: 'Phone', value: 'phone', visible: true },
  ]);

  const apiUrl = useRuntimeConfig().public.apiUrl;
  const searchQuery = ref('');
  const sort = ref({ column: 'id', direction: 'asc' }); // Column and direction for sorting

  const { data: customers } = await useAsyncData(() =>
    $fetch(`${apiUrl}customers?_sort=${sort.value.column}&_order=${sort.value.direction}`)
  );

  // Computed para filtrar los customers basados en la búsqueda
  const filteredCustomers = computed(() => {
    if (!searchQuery.value) return customers.value; // Si no hay búsqueda, devolver todos los customers

    const lowerSearchQuery = searchQuery.value.toLowerCase();
    return customers.value.filter(customer => 
      customer.givenName.toLowerCase().includes(lowerSearchQuery) || 
      customer.familyName1.toLowerCase().includes(lowerSearchQuery) || 
      customer.email.toLowerCase().includes(lowerSearchQuery) ||
      customer.phone.toLowerCase().includes(lowerSearchQuery)
    );
  });

  // Computed para aplicar tanto el filtro como el orden
  const sortedFilteredCustomers = computed(() => {
    let filtered = filteredCustomers.value;
    
    // Ordenar los resultados según el valor de 'sort'
    if (sort.value.column && sort.value.direction) {
      filtered = filtered.sort((a, b) => {
        const aValue = a[sort.value.column];
        const bValue = b[sort.value.column];

        if (sort.value.direction === 'asc') {
          return aValue < bValue ? -1 : aValue > bValue ? 1 : 0;
        } else {
          return aValue < bValue ? 1 : aValue > bValue ? -1 : 0;
        }
      });
    }

    return filtered;
  });

  // Función para manejar el cambio de orden cuando se hace clic en las columnas
  const handleSort = (column) => {
    if (sort.value.column === column) {
      // Si se hace clic en la misma columna, alternamos la dirección
      sort.value.direction = sort.value.direction === 'asc' ? 'desc' : 'asc';
    } else {
      // Si se hace clic en una columna diferente, establecemos el nuevo orden ascendente
      sort.value.column = column;
      sort.value.direction = 'asc';
    }
  };

  // SEO
  useHead({
    title: 'Customers'
  });
</script>
