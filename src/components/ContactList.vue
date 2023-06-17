<script setup>
import { defineProps, computed, ref } from 'vue'
import ContactListItem from './ContactListItem.vue'

const props = defineProps(['contacts'])
const emit = defineEmits(['remove'])
const searchQuery = ref('')

const filteredContacts = computed(() => {
  if (!searchQuery.value) {
    return props.contacts
  }
  const query = searchQuery.value.toLowerCase()
  return props.contacts.filter((contact) => {
    const fullName = `${contact.firstName} ${contact.lastName}`.toLowerCase()
    return fullName.includes(query)
  })
})
</script>

<template>
  <div class="panel is-success">
    <div class="panel-heading">Contacts</div>
    <div class="panel-block">
      <input class="input" type="text" v-model="searchQuery" placeholder="Search contacts" />
    </div>
    <div class="panel-block is-flex is-flex-direction-column is-align-items-stretch">
      <div v-for="contact in filteredContacts" :key="contact.phoneNumber">
        <ContactListItem @remove="emit('remove', contact)" :contact="contact" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
