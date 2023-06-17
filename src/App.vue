<script setup>
import { ref } from 'vue'
import ContactForm from './components/ContactForm.vue'
import ContactList from './components/ContactList.vue'
import sampleData from './sampleData'

const contacts = ref(sampleData || JSON.parse(localStorage.getItem('contacts')))

const setContactsInLocalStorage = () => {
  localStorage.setItem('contacts', JSON.stringify(contacts.value))
}

const addContact = (contact) => {
  contacts.value = [...contacts.value, contact]
  setContactsInLocalStorage()
}
// const deleteContact = (contact) => {
//   contacts.value = contacts.value.filter((c) => c.id !== contact.id)
//   setContactsInLocalStorage()
// }
const deleteContact = (contact) => {
  const index = contacts.value.indexOf(contact)
  if (index !== -1) {
    contacts.value.splice(index, 1)
  }
}
</script>

<template>
  <h1 class="is-size-1 has-text-centered has-text-info">Vue Phonebook</h1>
  <div class="container px-4">
    <div class="columns">
      <div class="column">
        <ContactForm @submit="addContact" />
      </div>
      <div class="column">
        <ContactList :contacts="contacts" @remove="deleteContact" />
      </div>
      <div class="column"></div>
    </div>
  </div>
</template>

<style scoped></style>
