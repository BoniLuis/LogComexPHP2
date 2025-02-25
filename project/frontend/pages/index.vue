<template>
  <div class="home">
    <h1 class="title">Bem-vindo à PokéDex</h1>
    <p class="subtitle">Explore todos os Pokémon e descubra seus detalhes!</p>
    <NuxtLink to="/pokemonList" class="explore-button"
      >Explorar Pokémons</NuxtLink
    >
  </div>
</template>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.title {
  font-size: 48px;
  font-weight: bold;
  animation: fadeIn 1.5s ease-in-out;
}
.subtitle {
  font-size: 18px;
  margin-top: 10px;
  opacity: 0.9;
  animation: fadeIn 2s ease-in-out;
}
.explore-button {
  margin-top: 30px;
  padding: 15px 30px;
  font-size: 18px;
  font-weight: bold;
  color: var(--text-colors);
  background: var(--background-buttons);
  border-radius: 10px;
  text-decoration: none;
  transition: all 0.3s ease-in-out;
  animation: fadeIn 2.5s ease-in-out;
}
.explore-button:hover {
  background: var(--background-buttons-hover);
  transform: scale(1.05);
}
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
