<script setup>
import Footer from '../components/Footer.vue'
import { inject } from 'vue';

const user = inject("user");
</script>

<template>
    <div class="profile">
        <div v-if="user">
            <p>ID: {{ user.id }}</p>
            <p>Username: {{ user.username || "No data" }}</p>
            <p>Firstname: {{ user.first_name || "No data" }}</p>
            <p>Lastname: {{ user.last_name || "No data" }}</p>
            <p>Balance: {{ user.balance }}</p>
            <p>Victories: {{ user.victories }}</p>
            <p>Refferel_code: {{ user.referral_code }}</p>
        </div>
        <div v-else>
            <h1>Loading...</h1>
        </div>
    </div>
    <Footer />
</template>

<style scoped>
.profile {
    width: 100%;
    padding: 20px;
}
</style>