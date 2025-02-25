<template>
  <header class="header">
    <div class="logo">
      <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png" alt="Pikachu Logo" />
    </div>
    <nav>
      <NuxtLink class="item" to="/"> Home </NuxtLink>
      <NuxtLink class="item" to="/pokemonList"> Pokémons </NuxtLink>
    </nav>
  </header>
</template>

<script setup lang="ts">
import { NuxtLink } from "#components";
</script>

<style scoped>
.header {
  width: 100%;
  display: flex;
  align-items: center;
  padding: 15px 40px;
  height: 50px;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.2);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
}

.logo img {
  width: 60px;
  height: 60px;
  object-fit: contain;
  transition: transform 0.3s ease-in-out;
}

nav {
  display: flex;
  gap: 30px;
}

.item {
  font-size: 18px;
  font-weight: bold;
  color: #fff;
  text-decoration: none;
  padding: 10px 20px;
  border-radius: 8px;
  transition: all 0.3s ease-in-out;
}

.item:first-child {
  margin-left: 15px;
}

.item:hover {
  background: linear-gradient(135deg, #ffcc00, #ff5722);
  transform: scale(1.05);
  color: #fff;
}
</style>
