<template>
    <header class="flex flex-col gap-4 text-xl w-3/4 mx-auto py-4">
        <div class="flex justify-between">
            <NuxtLink to="/">Joseperezdmgz</NuxtLink>
            <a href="https://github.com/joseperezdmgz/project-repo" target="_blank">Github</a>
        </div>
        <nav class="flex gap-4">
            <template v-for="item in menu">
                <NuxtLink :to="item.path" class="hover:text-gray-500 hover:border-b-2" activeClass="border-b-2 border-black transition-all duration-300">{{ item.name }}</NuxtLink>
            </template>
        </nav>
    </header>
    <hr/>
</template>

<script setup>
    const menu = ref([
        { name:'Home', path: '/' },
        { name:'Customers', path: '/customers' },
        { name:'Products', path: '/products' },
    ])
</script>