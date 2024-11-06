<template>
  <input
    v-model="searchQuery"
    @input="handleSearch"
    placeholder="Search by name"
    class=" p-2 h-10 bg-white border focus:outline focus:outline-1 focus:outline-white"
  />
</template>

<script setup lang="ts">
import { ref } from 'vue'

const searchQuery = ref('')

const emit = defineEmits(['search'])

const handleSearch = () => {
  emit('search', searchQuery.value)
}
</script>
