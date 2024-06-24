<template>
  <div>
    <NuxtLink to="/people" class="text-yellow-400 hover:underline mb-5 block">Back to Overview</NuxtLink>
    <div v-if="fetchError">
      <span class="text-yellow-400">Error loading person</span>
    </div>
    <div v-else-if="isFetching">
      <span class="text-yellow-400">Loading...</span>
    </div>
    <div v-else>
      <div class="bg-black text-white border-yellow-400 border-2 rounded-xl p-5 text-center h-full w-full bg-clip-padding backdrop-filter backdrop-blur-sm bg-opacity-50">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <h2 class="text-white text-xl mb-2">Overview of {{ person.name }}</h2>
            <ul class="list-none list-inside">
              <li>Height: {{ person.height }} cm</li>
              <li>Mass: {{ person.mass }} kg</li>
              <li>Hair color: {{ person.hair_color }}</li>
              <li>Skin color: {{ person.skin_color }}</li>
              <li>Eye color: {{ person.eye_color }}</li>
              <li>Birth year: {{ person.birth_year }}</li>
              <li>Gender: {{ person.gender }}</li>
            </ul>
          </div>
          <div>
            <h3 class="text-xl mt-2 mb-2">Appears in:</h3>
            <ul class="list-none list-inside">
              <li v-for="film in person.films" :key="film">{{ getFilmTitle(film) }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>

const route = useRoute()
const { id } = route.params

const { data: person, isFetching, error: fetchError } = await useFetch(`https://swapi.dev/api/people/${id}/`)

const getFilmTitle = (url) => {
  const filmId = url.split('/').slice(-2, -1)[0];
  const filmTitles = {
    1: 'A New Hope',
    2: 'The Empire Strikes Back',
    3: 'Return of the Jedi',
    4: 'The Phantom Menace',
    5: 'Attack of the Clones',
    6: 'Revenge of the Sith',
  };
  return filmTitles[filmId] || 'Unknown Film';
};

</script>

<style scoped>
ul li {
  color: #FACC15;
}
</style>