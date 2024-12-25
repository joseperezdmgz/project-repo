<template>
  <div>
    <UserDetails :details="customers[0]"/>
    <h2 class="text-xl my-6">Productos contratados:</h2>
    <ul class="flex gap-4">
      <template v-for="product in products" >
        <Card :details="product"/>
      </template>
    </ul>
  </div>
</template>


<script setup>
  const route = useRoute();
  const customerId = route.params.id;
  const apiUrl = useRuntimeConfig().public.apiUrl;
  const { data: customers } = await useAsyncData(() => $fetch(`${apiUrl}customers?customerId=${customerId}`));
  const { data: products } = await useAsyncData(() => $fetch(`${apiUrl}products?customerId=${customerId}`));

  // Cambia el título de la página dinamicamente
  watch(customers, (newCustomers) => {
    if (newCustomers) {
      useHead({
        title: `${newCustomers[0].givenName} ${newCustomers[0].familyName1} - Detalles`,
      });
    }
  }, { immediate: true });

</script>
