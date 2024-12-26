<template>
  <div class="max-w-4xl mx-auto p-6 bg-white rounded-lg shadow-lg">
    <h1 class="text-3xl font-bold text-center text-gray-800 mb-6">
      PRUEBA TÉCNICA - FRONT-END VUE.JS
    </h1>
    <p class="text-lg text-gray-700 mb-6">
      El proyecto está diseñado para interactuar con una API simulada, mostrando productos de manera dinámica y eficiente.
    </p>
    <p class="text-xl font-semibold text-gray-800 mb-4">Stack utilizado:</p>
    <ul class="list-disc pl-6 mb-6 text-gray-700">
      <li><strong>Nuxt 3</strong> - Framework basado en Vue.js para crear aplicaciones web rápidas y eficientes.</li>
      <li><strong>JSON Server</strong> - API simulada para gestionar datos durante el desarrollo.</li>
      <li><strong>Tailwind CSS</strong> - Framework de utilidades para crear interfaces modernas y responsivas.</li>
    </ul>

    <div class="text-center mb-6">
      <p class="text-lg text-gray-800">
        <strong>Para probar la API, haz clic en el siguiente enlace:</strong>
      </p>
      <a :href="apiUrl" target="_blank" class="inline-block mt-4 px-6 py-3 text-white bg-blue-500 rounded-lg text-xl hover:bg-blue-600 transition duration-200">
        Probar API
      </a>
    </div>
    <footer class="text-center text-gray-600 text-sm">
      <p>Creado por Jose - 26/12/2024</p>
    </footer>
  </div>
</template>

<script setup>
  const apiUrl = useRuntimeConfig().public.apiUrl;
  useHead({
      title: 'Prueba Técnica - Front-End Vue.js'
  });
</script>