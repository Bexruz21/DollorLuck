<script setup>
import { inject } from 'vue';

const user = inject("user");
</script>

<template>
    <div class="profile">
        <div v-if="user">
            <p>ID: {{ user.id }}</p>
            <p>Username: {{ user.username || " " }}</p>
            <p>Имя: {{ user.first_name || " " }}</p>
            <p>Фамилия: {{ user.last_name || " " }}</p>
            <p>Баланс: {{ user.balance }}</p>
            <p>Победы: {{ user.victories }}</p>
            <p>Реферальная ссылка: "https://t.me/dollorluck_bot?start={{ user.referral_code }}"</p>
        </div>
        <div v-else>
            <h1>Загрузка...</h1>
        </div>
    </div>
</template>

<style scoped>
.profile {
    width: 100%;
    padding: 20px;
}
</style>