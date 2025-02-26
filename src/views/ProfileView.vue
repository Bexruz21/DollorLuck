<script setup>
import Footer from '../components/Footer.vue'
import { inject } from 'vue';

const user = inject("user");
</script>

<template>
  <div v-if="user">
    <h1>ID: {{ user.id }}</h1>
    <h1>Username: {{ user.username || "No data" }}</h1>
    <h1>Firstname: {{ user.first_name || "No data" }}</h1>
    <h1>Lastname: {{ user.last_name || "No data" }}</h1>
  </div>
  <div v-else>
    <h1>Loading...</h1>
  </div>
  <Footer/>
</template>