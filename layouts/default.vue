<template>
    <div class="container mx-auto">
    <div class="nav flex flex-row gap-5 justify-center">
        <NuxtLink to="/">Home</NuxtLink>
        <NuxtLink to="/people">People</NuxtLink>
        <NuxtLink to="/starships">Starships</NuxtLink>
    </div>
    <hr class="mt-2 mb-2">
        <slot/>
    </div>
</template>

<script setup>

</script>

<style  scoped>
    .nav a {
        color: #000;
        font-size: 30px;
        transition: color 0.5s;
            -webkit-text-stroke-width: 0.5px;
            -webkit-text-stroke-color: #FACC15;
    }

    .nav a:hover {
        color: #FACC15;
    }

    a.router-link-active.router-link-exact-active {
        color: #FACC15;
    }
</style>