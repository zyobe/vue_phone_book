<script setup lang="ts">
import { ref, computed } from 'vue'

interface entryObj {
  firstName: string
  lastName: string
  phone: string | number
}

const entry = ref<entryObj>({
  firstName: 'Coder',
  lastName: 'Byte',
  phone: '8885559999'
})

const entries = ref<entryObj[]>([])

const addItem = () => {
  entries.value.push({
    firstName: entry.value.firstName,
    lastName: entry.value.lastName,
    phone: entry.value.phone
  })
}

const sortEntries = computed(() =>
  [...entries.value].sort((a, b) => {
    if (a.lastName.toLowerCase() < b.lastName.toLowerCase()) {
      return -1
    }
    if (a.lastName.toLowerCase() > b.lastName.toLowerCase()) {
      return 1
    }
    return 0
  })
)
</script>

<template>
  <div id="app">
    <h1>Phone book</h1>
    <p class="phonebook-title"><strong>Add a new contact:</strong></p>

    <div class="phonebook">
      <div class="add-entry">
        <div class="add-entry__inputs">
          <label class="add-entry__label">
            First Name:
            <input type="text" class="userFirstname add-entry__input" v-model="entry.firstName" />
          </label>
          <label class="add-entry__label">
            Last Name:
            <input type="text" class="userLastname add-entry__input" v-model="entry.lastName" />
          </label>
          <label class="add-entry__label">
            Phone:
            <input type="number" class="userPhone add-entry__input" v-model="entry.phone" />
          </label>
        </div>
        <button class="submitButton" @click.prevent="addItem">Add New Contact</button>
      </div>
      <table v-if="entries.length > 0" id="phoneBookItems" class="informationTable entry-table">
        <thead>
          <tr class="entry-table__head">
            <th scope="col" class="entry-table__cell">First Name</th>
            <th scope="col" class="entry-table__cell">Last Name</th>
            <th scope="col" class="entry-table__cell">Phone</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(entry, index) in sortEntries" :key="index" class="entry-table__row">
            <th scope="row" class="entry-table__cell">{{ entry.firstName }}</th>
            <td class="entry-table__cell">{{ entry.lastName }}</td>
            <td class="entry-table__cell">{{ entry.phone }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.phonebook {
  align-items: flex-start;
  display: flex;
  gap: 10px;
}

.phonebook-title {
  font-family: sans-serif;
  font-size: 0.9em;
}

.add-entry {
  border: 1px solid #ccc;
  border-radius: 3px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
  display: flex;
  flex-basis: 25%;
  flex-direction: column;
  font-family: sans-serif;
  font-size: 0.9em;
  margin-bottom: 10px;
  padding: 10px;
}

.add-entry__label {
  display: block;
  margin-bottom: 10px;
}

.add-entry__input {
  border: 1px solid rgb(21 128 61);
  border-radius: 3px;
  padding: 5px;
}

.submitButton {
  align-self: start;
  background: rgb(21 128 61);
  border: 0;
  color: rgb(255 255 255);
  cursor: pointer;
  padding: 10px;
  text-transform: uppercase;
  transition: 0.3s;
}

.submitButton:hover {
  background: rgb(2 44 34);
}

.entry-table {
  border: 1px solid #ccc;
  border-collapse: collapse;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
  flex-basis: 75%;
  font-size: 0.9em;
  font-family: sans-serif;
  margin: 0 25px 0;
  min-width: 400px;
  width: 100%;
}

.entry-table__head {
  background-color: rgb(2 44 34);
  color: #fff;
  text-align: left;
}

.entry-table__cell {
  padding: 12px 15px;
  text-align: left;
}

.entry-table__row {
  border-bottom: 1px solid #ddd;
}

.entry-table__row:nth-of-type(even) {
  background-color: #f3f3f3;
}
</style>
