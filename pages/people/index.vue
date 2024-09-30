<template>
  <div class="container mx-auto">
      <h2>Overview of people</h2>
      <div class="filters">
          <div class="filters_gender mb-5">
              <div class="text-xl text-yellow-400">Genders</div>
              <label>
                  <input type="radio" value="" v-model="selectedGender" @change="filterByGender" /> Show All
              </label>
              <label>
                  <input type="radio" value="male" v-model="selectedGender" @change="filterByGender" /> Male
              </label>
              <label>
                  <input type="radio" value="female" v-model="selectedGender" @change="filterByGender" /> Female
              </label>
              <label>
                  <input type="radio" value="others" v-model="selectedGender" @change="filterByGender" /> Others
              </label>
          </div>
          
          <div class="filters_age mb-5">
              <div class="text-xl text-yellow-400 mb-2">Age</div>
              <button @click="filterByBirthYear" class="bg-black text-white border-yellow-400 border-2 px-4 py-2 rounded">Filter 20-40 BBY</button>
              <button @click="resetFilter" class="bg-gray-900 text-white px-4 border-yellow-400 border-2 py-2 rounded ml-2">Reset Filter</button>
          </div>
      </div>
      <div v-if="error">{{ error }}</div>
      <div v-else-if="isFetching" class="fetching text-xl text-yellow-400">Loading...</div>
      <div v-else class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
    
          <NuxtLink v-for="p in displayedPeople" :key="p.name" :to="`/people/${p.url.split('/').slice(-2, -1)[0]}`">
                  <PeopleCard :info="p" />
          </NuxtLink>
      </div>
      <div class="flex justify-center mt-5">
              <button v-if="!isFetching && nextPage" @click="loadMore" class="animate-bounce bg-black text-yellow-400 p-3 border-yellow-400 border-2 rounded-xl mb-10">Load More</button>
      </div>
      <div v-if="isFetching" class="flex justify-center mt-10 mb-10">Loading more...</div>
  </div>
</template>
<script setup>
const people = ref([]);
const displayedPeople = ref([]);
const selectedGender = ref('');
const currentPage = ref(1);
const nextPage = ref(null);
const { isFetching, error } = useFetch(`https://swapi.dev/api/people/?page=${currentPage.value}`);
const loadPeople = async () => {
  const response = await $fetch(`https://swapi.dev/api/people/?page=${currentPage.value}`);
  if (response) {
      people.value = [...people.value, ...response.results];
      displayedPeople.value = people.value;
      nextPage.value = response.next;
      filterPeople();
  }
};
onMounted(() => {
  loadPeople();
});
const filterPeople = () => {
  let filtered = people.value;
  if (selectedGender.value) {
      if (selectedGender.value === 'others') {
          filtered = filtered.filter(person => person.gender !== 'male' && person.gender !== 'female');
      } else {
          filtered = filtered.filter(person => person.gender === selectedGender.value);
      }
  }
  displayedPeople.value = filtered;
};
const filterByBirthYear = () => {
displayedPeople.value = people.value.filter(p => {
  const birthYear = p.birth_year;
  if (birthYear.endsWith('BBY')) {
    const year = parseFloat(birthYear);
    return year >= 20 && year <= 40;
  }
  return false;
});
};
watch(selectedGender, filterPeople);
const loadMore = () => {
  if (nextPage.value) {
      currentPage.value += 1;
      loadPeople();
  }
};
const resetFilter = () => {
displayedPeople.value = people.value;
};
</script>
<style  scoped>
 label {
  color: #FACC15;
  margin-right: 10px;
 }
</style>