<template>
  <div class="container mx-auto p-4">
    <div class="flex justify-between items-center">
      <h1 class="text-3xl font-bold w-1/2">Contact Management</h1>
      <SearchBar @search="handleSearch" class="w-1/2" />
    </div>

    <ContactForm ref="contactForm" @addContact="addContact" @updateContact="updateContact" class="mt-3" />
    <div class="mt-4 text-center" v-if="contacts.length <= 0">There are no contacts</div>
    <ContactList v-else :contacts="filteredContacts" @deleteContact="deleteContact" @editContact="editContact" />
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import ContactList from '@/components/ContactList.vue';
import ContactForm from '@/components/ContactForm.vue';
import SearchBar from '@/components/SearchBar.vue';

interface Contact {
  id: number;
  name: string;
  phone: string;
  email: string;
}

const contacts = ref<Contact[]>([]);
const searchQuery = ref('');
const contactForm = ref<InstanceType<typeof ContactForm> | null>(null);

const filteredContacts = computed(() => {
  return contacts.value.filter(contact => contact.name.toLowerCase().includes(searchQuery.value.toLowerCase()));
});

const handleSearch = (query: string) => {
  searchQuery.value = query;
};

const addContact = (contact: Contact) => {
  contacts.value.push(contact);
  saveContacts();
};

const updateContact = (updatedContact: Contact) => {
  const index = contacts.value.findIndex(contact => contact.id === updatedContact.id);
  if (index !== -1) {
    contacts.value[index] = updatedContact;
    saveContacts();
  }
};

const deleteContact = (id: number) => {
  contacts.value = contacts.value.filter(contact => contact.id !== id);
  saveContacts();
};

const editContact = (id: number) => {
  const contact = contacts.value.find(contact => contact.id === id);
  if (contact && contactForm.value) {
    contactForm.value.editContact(contact);
  }
};

const saveContacts = () => {
  localStorage.setItem('contacts', JSON.stringify(contacts.value));
};

const loadContacts = () => {
  const storedContacts = localStorage.getItem('contacts');
  if (storedContacts) {
    contacts.value = JSON.parse(storedContacts);
  }
};

loadContacts();
</script>

<style scoped>
/* Add any scoped styles here */
</style>
