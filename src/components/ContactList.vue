<template>
  <div class="mt-3">
    <transition-group name="list" tag="div">
      <ContactItem
        v-for="contact in contacts"
        :key="contact.id"
        :contact="contact"
        @deleteContact="deleteContact"
        @editContact="editContact"
      />
    </transition-group>
  </div>
</template>

<script setup lang="ts">
import ContactItem from './ContactItem.vue'

interface Contact {
  id: number
  name: string
  phone: string
  email: string
}

defineProps<{
  contacts: Contact[]
}>()

const emit = defineEmits(['deleteContact', 'editContact'])

const deleteContact = (id: number) => {
  emit('deleteContact', id)
}

const editContact = (id: number) => {
  emit('editContact', id)
}
</script>
<style scoped>
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
