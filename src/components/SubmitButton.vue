<!-- ActionButton.vue -->
<template>
  <button @click="handleClick" class="mr-2 bg-blue-500 px-4 py-1 rounded text-base text-white hover:bg-blue-600">
    {{ props.label }}
  </button>
</template>

<script setup lang="ts">

const props = defineProps<{
  label: string
}>()
const emit = defineEmits(['click'])

const handleClick = () => {
  emit('click')
}

</script>
