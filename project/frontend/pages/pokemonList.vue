<template>
  <div class="container">
    <h1>Lista de Pokémons</h1>
    <div class="filters-container">
      <Filter v-model="search" class="filter-item" @input="onInputChange" />
      <TypeFilter
        v-model="selectedType"
        class="filter-item"
        @input="onInputChange"
      />
    </div>

    <div v-if="isLoading" class="loading-container">
      <h1>Carregando...</h1>
    </div>

    <div v-else class="grid">
      <CardItem
        v-for="pokemon in filteredPokemons"
        :key="pokemon.id"
        :pokemon="pokemon"
      />
    </div>

    <Pagination
      v-if="!isLoading && filteredPokemons.length > 0"
      v-model:page="page"
      :total="total"
      :limit="limit"
      :last-page="lastPage"
      @update:page="fetchPokemons"
    />
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from "vue";
import axios from "axios";
import CardItem from "~/components/cardItem.vue";
import Pagination from "~/components/pagination.vue";
import Filter from "~/components/filter.vue";
import TypeFilter from "~/components/typeFilter.vue";

const pokemons = ref([]);
const page = ref(1);
const limit = ref(30);
const total = ref(0);
const lastPage = ref(0);
const search = ref("");
const selectedType = ref("");
const isLoading = ref(false);
let debounceTimeout = null;

const fetchPokemons = async () => {
  isLoading.value = true;
  try {
    const response = await axios.get(
      "http://localhost:8000/api/admin/pokemons",
      {
        params: {
          filter: search.value,
          type: selectedType.value,
          page: page.value,
          perPage: limit,
        },
      }
    );

    pokemons.value = response.data.data;
    total.value = response.data.total;
    lastPage.value = response.data.last_page;
    page.value = response.data.current_page;
  } catch (error) {
    console.error("Erro ao buscar Pokémons:", error);
  } finally {
    isLoading.value = false;
  }
};

const onInputChange = () => {
  clearTimeout(debounceTimeout);
  debounceTimeout = setTimeout(() => {
    page.value = 1;
    fetchPokemons();
  }, 1000);
};

onMounted(fetchPokemons);

const filteredPokemons = computed(() => pokemons.value);
</script>

<style scoped>
.container {
  padding: 100px 15px 30px;
}
h1 {
  text-align: center;
  margin-bottom: 20px;
}
.filter-item {
  max-width: 250px;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 20px;
}
</style>
