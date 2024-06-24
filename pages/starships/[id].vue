<template>
    <div>
        <NuxtLink to="/starships" class="text-yellow-400 hover:underline mb-5 block">Back to Overview</NuxtLink>
        <div v-if="fetchError">
            <span class="text-yellow-400">Error loading spaceships</span>
        </div>
        <div v-else-if="isFetching">
            <span class="text-yellow-400">Loading...</span>
        </div>
        <div v-else>
            <div class="bg-black text-white border-yellow-400 border-2 rounded-xl p-5 text-center h-full w-full bg-clip-padding backdrop-filter backdrop-blur-sm bg-opacity-50">
                <h2 class="text-yellow-400 text-xl">Overview of {{ ship.name }}</h2>
                <ul>
                    <li>Model: {{ ship.model }}</li>
                    <li>Manufacturer: {{ ship.manufacturer }}</li>
                    <li>Cost in Credits: {{ ship.cost_in_credits }}</li>
                    <li>Length: {{ ship.length }}</li>
                    <li>Max Atmosphering Speed: {{ ship.max_atmosphering_speed }}</li>
                    <li>Crew: {{ ship.crew }}</li>
                    <li>Passengers: {{ ship.passengers }}</li>
                    <li>Cargo Capacity: {{ ship.cargo_capacity }}</li>
                    <li>Consumables: {{ ship.consumables }}</li>
                    <li>Hyperdrive Rating: {{ ship.hyperdrive_rating }}</li>
                    <li>MGLT: {{ ship.MGLT }}</li>
                    <li>Starship Class: {{ ship.starship_class }}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script setup>

const route = useRoute()
const { id } = route.params

const { data: ship, isFetching, error: fetchError } = await useFetch(`https://swapi.dev/api/starships/${id}/`)
</script>

<style scoped>
    ul li {
        color: #FACC15;
    }
</style>