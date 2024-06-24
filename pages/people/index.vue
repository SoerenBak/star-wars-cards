<template>
    <div>
        <h2 class="text-5xl text-yellow-400 mb-4">Overview of people:</h2>
        <div v-if="fetchError">
            <span class="text-red-600">Error loading people</span>
        </div>
        <div v-else-if="isFetching">
            <span class="text-yellow-400">Loading...</span>
        </div>
        <div v-else>
        <div class="mb-5">
            <button @click="resetFilters" class="bg-yellow-400 text-black p-2 rounded mr-2">Show All</button>
            <button @click="filterByAge" class="bg-yellow-400 text-black p-2 rounded mb-2">Filter by age 20-40 BBY</button>
            <label for="gender" class="block mb-2 text-yellow-400">Filter by gender:</label>
            <select id="gender" v-model="selectedGender" class="bg-black p-2 border border-yellow-400 rounded text-yellow-400">
                <option value="">All</option>
                <option value="male">Male</option>
                <option value="female">Female</option>
                <option value="n/a">Other</option>
            </select>
      </div>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
                <NuxtLink v-for="person in filteredPeople" :key="person.name" :to="`/people/${person.url.split('/').slice(-2, -1)[0]}`">                  
                       <PeopleCard :info="person"/>
                </NuxtLink>
            </div>
        </div>

        <div v-if="nextPage">
            <div class="flex justify-center">
                <button @click="loadMore" class="bg-yellow-400 text-black p-2 rounded mt-5">Load More</button>
            </div>
        </div>
       
    </div>
</template>

<script setup>
const people = ref([])
const nextPage = ref('https://swapi.dev/api/people')
const isFetching = ref(false)
const fetchError = ref(null)

const selectedGender = ref('')
const filterByAgeFlag = ref(false)

const fetchPeople = async (url) => {
  isFetching.value = true
  try {
    const response = await fetch(url)
    const data = await response.json()
    people.value = [...people.value, ...data.results]
    nextPage.value = data.next
  } catch (error) {
    fetchError.value = error.message
  } finally {
    isFetching.value = false
  }
}

await fetchPeople(nextPage.value)

const filteredPeople = computed(() => {
  if (!people.value) return []

  let result = people.value

  if (selectedGender.value) {
    result = result.filter(person => person.gender === selectedGender.value)
  }

  if (filterByAgeFlag.value) {
    result = result.filter(person => {
      const birthYear = person.birth_year
      const year = parseFloat(birthYear)
      return birthYear.endsWith('BBY') && year >= 20 && year <= 40
    })
  }
  return result
})

const filterByAge = () => {
  filterByAgeFlag.value = !filterByAgeFlag.value
}

const resetFilters = () => {
  selectedGender.value = ''
  filterByAgeFlag.value = false
}

const loadMore = async () => {
  if (nextPage.value) {
    await fetchPeople(nextPage.value)
  }
}
</script>

<style scoped>

</style>