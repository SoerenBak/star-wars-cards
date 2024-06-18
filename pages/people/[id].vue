<template>
    <div class="container mx-auto py-10">
      <NuxtLink to="/people" class="text-yellow-400 hover:underline mb-5 block">Back to Overview</NuxtLink>
      <div v-if="error" class="text-red-500">{{ error }}</div>
      <div v-else-if="isFetching" class="text-yellow">Loading...</div>
      <div v-else-if="person" class="bg-black p-10 rounded-lg border-yellow-400 border-2 shadow-md text-yellow-400">
        <h2 class="text-3xl font-bold mb-5">{{ person.name }}</h2>
        <div class="grid grid-cols-2 gap-4">
          <div>
            <h3 class="text-xl font-semibold mb-2">General Information</h3>
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
            <h3 class="text-xl font-semibold mb-2">Films</h3>
            <ul class="list-disc list-inside">
              <li v-for="film in person.films" :key="film">{{ getFilmTitle(film) }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  
  const route = useRoute();
  const person = ref(null);
  const error = ref(null);
  const isFetching = ref(true);
  
  const fetchPerson = async () => {
  console.log('Fetching person data for ID:', route.params.id);
  isFetching.value = true;
  
  const { data, error: fetchError } = await useFetch(`https://swapi.dev/api/people/${route.params.id}/`);

  if (fetchError.value) {
    console.log('Error fetching data:', fetchError.value);
    error.value = fetchError.value;
  } else {
    console.log('Fetched data:', data.value);
    person.value = data.value;
  }

  isFetching.value = false;
  console.log('Fetching complete');
};
  
  watch(route, () => {
    fetchPerson();
  });
  
  onMounted(() => {
    fetchPerson();
  });
  
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
  .container {
    padding: 20px;
  }
  </style>
  