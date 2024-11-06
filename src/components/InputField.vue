<!-- InputField.vue -->
<template>
  <div class="flex-1">
    <input
      v-model="modelValue"
      @input="updateValue"
      :placeholder="placeholder"
      class="w-full border px-2 py-1 focus:outline focus:outline-1 focus:outline-white"
    />
    <div v-for="error of errors" class="text-red-500 text-xs">{{ error.$message }}</div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'

const props = defineProps<{
  modelValue: string
  placeholder: string
  errors: any[]
}>()

const emit = defineEmits(['update:modelValue'])

const modelValue = ref(props.modelValue)

const updateValue = (event: Event) => {
  const target = event.target as HTMLInputElement
  modelValue.value = target.value
  emit('update:modelValue', modelValue.value)
}

watch(
  () => props.modelValue,
  (newVal) => {
    modelValue.value = newVal
  },
)
</script>
