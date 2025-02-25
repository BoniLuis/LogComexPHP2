<template>
  <div v-if="pokemon" class="pokemon-container">
    <div class="pokemon-image">
      <img
        v-if="hasImage"
        :src="`https://img.pokemondb.net/sprites/home/normal/${pokemon.name.toLowerCase()}.png`"
        :alt="pokemon.name"
        @error="hasImage = false"
      />
      <div v-else class="image-placeholder">Sem imagem</div>
    </div>

    <div class="pokemon-info">
      <h2 class="pokemon-name">{{ pokemon.name }}</h2>

      <div class="pokemon-details">
        <div class="info-row">
          <span>Altura:</span>
          <span class="info-box">{{ pokemon.height_cm }} cm</span>
        </div>
        <div class="info-row">
          <span>Peso:</span>
          <span class="info-box">{{ pokemon.weight_kg }} kg</span>
        </div>
      </div>
      <div class="info-row">
        <span>Tipo</span>
        <div :class="['type-container', pokemon.type]">
          {{ pokemon.type }}
        </div>
      </div>
    </div>
    <NuxtLink class="button-back" to="/pokemonList">Voltar</NuxtLink>
  </div>

  <div v-if="isLoading" class="loading-container">
    <h1>Carregando...</h1>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";

const route = useRoute();
const pokemon = ref(null);
const isLoading = ref(true);
const error = ref(null);
const hasImage = ref(true);

const fetchPokemon = async () => {
  isLoading.value = true;
  hasImage.value = true;
  try {
    const response = await axios.get(
      `http://localhost:8000/api/admin/pokemons/${route.params.id}`
    );
    pokemon.value = response.data;
  } catch (err) {
    error.value = err;
    console.error(err);
  } finally {
    isLoading.value = false;
  }
};

onMounted(fetchPokemon);

watch(() => route.params.id, fetchPokemon);
</script>

<style scoped>
.pokemon-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 40px;
  background: linear-gradient(135deg, #2c3e50, #34495e);
  border-radius: 15px;
  box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.2);
  max-width: 400px;
  margin: 100px auto;
  text-align: center;
}
.pokemon-image img {
  width: 150px;
  height: 150px;
  object-fit: contain;
  border-radius: 50%;
  background-color: #fff;
  padding: 10px;
  box-shadow: 0px 4px 10px rgba(255, 255, 255, 0.3);
}
.pokemon-name {
  font-size: 24px;
  color: #ffcb05;
  text-transform: capitalize;
  margin-top: 10px;
}
.pokemon-info {
  width: 100%;
  margin-top: 15px;
}
.info-row {
  display: flex;
  justify-content: space-between;
  background: rgba(255, 255, 255, 0.1);
  padding: 10px 15px;
  border-radius: 8px;
  margin: 5px 0;
  font-size: 18px;
  color: #fff;
  height: 25px;
}
.info-box {
  font-weight: bold;
  color: #fff;
}
.type-container {
  display: flex;
  gap: 8px;
  padding: 5px 10px;
  border-radius: 8px;
  font-weight: bold;
  color: #fff;
  text-transform: capitalize;
  font-size: 14px;
}
.fire {
  background: var(--fire-gradient);
}
.water {
  background: var(--water-gradient);
}
.grass {
  background: var(--grass-gradient);
}
.electric {
  background: var(--electric-gradient);
  color: var(--text-dark);
}
.ice {
  background: var(--ice-gradient);
}
.fighting {
  background: var(--fighting-gradient);
}
.poison {
  background: var(--poison-gradient);
}
.ground {
  background: var(--ground-gradient);
}
.flying {
  background: var(--flying-gradient);
  color: var(--text-dark);
}
.psychic {
  background: var(--psychic-gradient);
}
.bug {
  background: var(--bug-gradient);
}
.rock {
  background: var(--rock-gradient);
}
.ghost {
  background: var(--ghost-gradient);
}
.dragon {
  background: var(--dragon-gradient);
}
.dark {
  background: var(--dark-gradient);
}
.steel {
  background: var(--steel-gradient);
}
.fairy {
  background: var(--fairy-gradient);
}

.button-back {
  text-align: center;
  color: #fff;
  background: var(--background-buttons);
  padding: 10px 20px;
  border-radius: 8px;
  text-decoration: none;
  font-weight: bold;
  transition: all 0.3s ease-in-out;
  margin-top: 20px;
}
.button-back:hover {
  background: var(--background-buttons-hover);
  transform: scale(1.05);
}
.loading-container {
  text-align: center;
  margin-top: 120px;
  font-size: 18px;
  color: #fff;
}
</style>
