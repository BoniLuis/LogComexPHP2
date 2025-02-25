<template>
  <div class="type-filter">
    <label for="type-select">Filtrar por Tipo:</label>
    <select id="type-select" :value="selectedType" @change="emitChange">
      <option value="">Todos</option>
      <option v-for="type in types" :key="type" :value="type">
        {{ type }}
      </option>
    </select>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue"

const types = ref([])

const selectedType = defineModel()

const fetchTypes = async () => {
  const response = await fetch("https://pokeapi.co/api/v2/type")
  const data = await response.json()
  types.value = data.results.map(t => t.name)
}

const emit = defineEmits(["input"])

const emitChange = (event) => {
  selectedType.value = event.target.value
  emit('input', selectedType.value)
}

onMounted(fetchTypes)
</script>

<style scoped>
.type-filter {
  margin: 10px 5px;
}
label {
  font-weight: bold;
  margin-right: 8px;
}
select {
  width: 100px;
  padding: 5px;
  border: 1px solid var(--border-color);
  border-radius: 5px;
  background-color: var(--background-header-color);
  color: var(--text-color);
}
</style>
