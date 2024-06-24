<template>
    <div>
        <h2>Overview of starships</h2>
        <div v-if="fetchError">
            <span class="text-yellow-400">Error loading spaceships</span>
        </div>
        <div v-else-if="isFetching">
            <span class="text-yellow-400">Loading...</span>
        </div>
        <div v-else>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
                <NuxtLink v-for="ship in starships.results" :key="ship.name" :to="`/starships/${ship.url.split('/').slice(-2, -1)[0]}`">
                    <div class="bg-black text-white border-yellow-400 border-2 rounded-xl p-5 text-center h-full w-full bg-clip-padding backdrop-filter backdrop-blur-sm bg-opacity-50">
                        <h1 class="text-yellow-400">{{ ship.name }}</h1>
                    </div>
                </NuxtLink>
            </div>
        </div>
       
    </div>
</template>

<script setup>
    const { data: starships, isFetching, error: fetchError } = await useFetch('https://swapi.dev/api/starships')
</script>