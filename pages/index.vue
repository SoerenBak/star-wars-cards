<template>
    <div class="h-screen flex items-center justify-center flex-col gap-y-5">
        <h1 class="text-5xl text-yellow-400 text-center">Star Wars</h1>
        <NuxtLink to="/people/" class="text-3xl text-yellow-400 underline" >People</NuxtLink>
    </div>
</template>

<script setup>

</script>

<style>
 body {
    background-image: url(/assets/sw-bg.png);
 }

</style>