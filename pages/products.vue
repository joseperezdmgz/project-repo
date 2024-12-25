<template>
    <div>
      <h1>Products</h1>
      <DynamicTable :columns="columns" :rows="products" link=""/>
    </div>
  </template>
  
<script setup>
  const apiUrl = useRuntimeConfig().public.apiUrl;
  const { data:products } = await useAsyncData(() => 
    $fetch(`${apiUrl}products`)
  );

  const columns = ref([
    { name: 'id', value: 'id', visible: true },
    { name: 'productName', value: 'productName', visible: true },
    { name: 'mbSpeed', value: 'mbSpeed', visible: true },
    { name: 'gbData', value: 'gbData', visible: true },
    { name: 'productTypeName', value: 'productTypeName', visible: true },
    { name: 'numeracioTerminal', value: 'numeracioTerminal', visible: true },
    { name: 'soldAt', value: 'soldAt', visible: true },
    { name: 'customerId', value: 'customerId', visible: true },
  ]);
  

  useHead({
    title: 'Products'
  })
</script>