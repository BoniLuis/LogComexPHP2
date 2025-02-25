<template>
  <div class="card">
    <div class="image-container">
      <img
        v-if="hasImage"
        :src="`https://img.pokemondb.net/sprites/home/normal/${pokemon.name.toLowerCase()}.png`"
        :alt="pokemon.name"
        class="pokemon-image"
        @error="hasImage = false"
      />
      <div v-else class="image-placeholder">Sem imagem</div>
    </div>
    <h3>{{ pokemon.name }}</h3>
    <span class="type-badge">{{ pokemon.type }}</span>
    <NuxtLink class="detail-button" :to="`/pokemon/${pokemon.id}`">
      Detalhes
    </NuxtLink>
  </div>
</template>

<script setup>
import { defineProps } from "vue"

const props = defineProps({
  pokemon: {
    id: Number,
    name: String,
    type: String,
    height_cm: Number,
    weight_kg: String
  }
})

const hasImage = ref(true)
</script>

<style scoped>
.card {
  background: linear-gradient(135deg, #282c34, #3a3f4b);
  border-radius: 15px;
  padding: 15px;
  text-align: center;
  transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
  border: 1px solid #3a3f4b;
}
.card:hover {
  transform: scale(1.05);
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.3);
}
.image-placeholder {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 0.8rem;
  margin: 0 auto 10px auto;
}
.pokemon-image {
  width: 100px;
  height: 100px;
  object-fit: contain;
  margin-bottom: 10px;
}
h3 {
  color: #fff;
  text-transform: capitalize;
  font-size: 1.2rem;
}
.type-badge {
  display: inline-block;
  padding: 4px 10px;
  border-radius: 20px;
  background-color: rgba(255,255,255,0.2);
  font-size: 0.9rem;
  margin-bottom: 15px;
  text-transform: capitalize;
}
.detail-button {
  display: inline-block;
  margin-top: 10px;
  color: #fff;
  background: linear-gradient(135deg, #ffcb05, #ff9800);
  padding: 8px 15px;
  border-radius: 8px;
  text-decoration: none;
  font-weight: bold;
  transition: background 0.2s ease-in-out;
}
.detail-button:hover {
  background: linear-gradient(135deg, #ff9800, #ff7300);
}
</style>
