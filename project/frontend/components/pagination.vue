<template>
  <div class="pagination">
    <button @click="emit('update:page', props.page - 1)" :disabled="props.page === 1">
      Anterior
    </button>
    <span>Página {{ props.page }} de {{ props.lastPage }}</span>
    <button @click="emit('update:page', props.page + 1)" :disabled="props.page >= props.lastPage">
      Próxima
    </button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  page: Number,
  lastPage: Number
})

const emit = defineEmits(['update:page'])
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 20px;
}
button {
  padding: 8px 15px;
  border: none;
  background: #ff9800;
  color: #fff;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
}
button:hover {
  background: #f57c00;
}
button:disabled {
  background: #bdbdbd;
  cursor: not-allowed;
}
</style>
