<template>
  <input
    :value="props.modelValue"
    @input="emit('update:modelValue', $event.target.value)"
    placeholder="Filtrar por nome"
  />
</template>

<script setup>
import { defineProps, defineEmits } from "vue"
const props = defineProps({
  modelValue: String
})
const emit = defineEmits(["update:modelValue"])
</script>

<style scoped>
input {
  width: 30%;
  padding: 8px;
  margin-bottom: 20px;
  display: flex;
  margin: 0 auto 20px;
  background-color: var(--background-header-color);
  color: var(--text-color);
  border: 1px solid var(--border-color);
  border-radius: 5px;
}
input::placeholder {
  color: var(--text-color);
}
</style>
