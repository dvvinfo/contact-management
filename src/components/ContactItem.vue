<!-- ContactItem.vue -->
<template>
  <div class="border p-4 mb-2 flex flex-col gap-2">
    <h3 class="font-bold">{{ contact.name }}</h3>
    <p>{{ contact.phone }}</p>
    <p>{{ contact.email }}</p>
    <div class="flex items-center justify-end">
      <SubmitButton label="Edit"  @click="editContact" />
      <SubmitButton label="Delete" @click="deleteContact" />
    </div>
  </div>
</template>

<script setup lang="ts">
import SubmitButton from './SubmitButton.vue'

interface Contact {
  id: number
  name: string
  phone: string
  email: string
}

const props = defineProps<{
  contact: Contact
}>()

const emit = defineEmits(['deleteContact', 'editContact'])

const deleteContact = () => {
  emit('deleteContact', props.contact.id)
}

const editContact = () => {
  emit('editContact', props.contact.id)
}
</script>
