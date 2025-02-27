<script setup>
import Footer from '../components/Footer.vue'
import { inject } from 'vue';

const user = inject("user");
</script>

<template>
    <div class="profile">
        <div v-if="user">
            <p>{{ user }}</p>
            <p>ID: {{ user.id }}</p>
            <p>Username: {{ user.username || " " }}</p>
            <p>Имя: {{ user.first_name || " " }}</p>
            <p>Фамилия: {{ user.last_name || " " }}</p>
            <p>Баланс: {{ user.balance }}</p>
            <p>Победы: {{ user.victories }}</p>
            <p>Реферальная ссылка: {{ user.referral_code }}</p>
        </div>
        <div v-else>
            <h1>Загрузка...</h1>
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