<template>
    <div class="h-screen flex items-center justify-center flex-col gap-y-5">
        <NuxtLink to="/"><img src="../assets/sw-logo.png" class="logo" alt="Star wars logo"></NuxtLink>
        <NuxtLink to="/people/" class="text-3xl text-yellow-400 underline">People</NuxtLink>
        <NuxtLink to="/starships/" class="text-3xl text-yellow-400 underline">Starships</NuxtLink>
    </div>
</template>

<script setup>

</script>

<style>
 body {
    background-image: url(/assets/sw-bg.png);
 }

</style>
<style scoped>
    .logo {
        width: 250px;
        height: auto;
    }
</style>