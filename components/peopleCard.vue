<template>
    <div class="bg-black text-white border-yellow-400 border-2 rounded-xl p-5 text-center duration-500 hover:-translate-y-1 hover:shadow-2x">
        <p class="text-xl pb-5 text-yellow-400">{{ info.name }}</p>
        <ul>
            <li>Height: {{ info.height }}</li>
            <li>Mass: {{ info.mass }}</li>
            <li>Hair color: {{ info.hair_color }}</li>
            <li>Gender: {{ info.gender }}</li>
            <li>Birth year: {{ info.birth_year }}</li>
        </ul>
    </div>
</template>

<script setup>
    const { info } = defineProps(['info'])
</script>

<style scoped>

</style>