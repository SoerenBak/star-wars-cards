<template>
    <div class="bg-black text-white border-yellow-400 border-2 rounded-xl p-5 text-center duration-500 hover:-translate-y-1 hover:shadow-2x h-full w-full bg-clip-padding backdrop-filter backdrop-blur-sm bg-opacity-50">
        <p class="text-xl pb-2 text-yellow-400">{{ info.name }}</p>
        <ul>
            <li>Height: {{ info.height }}</li>
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