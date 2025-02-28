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
            <p>Ваш Рефераль: {{ user.referrer }}</p>
            <ul v-if="user.referrals.length">
                <li v-for="ref in user.referrals" :key="ref.telegram_id">
                    Имя: {{ ref.first_name }} (ID: {{ ref.telegram_id }})
                </li>
            </ul>
            <p v-else>У вас пока нет рефералов.</p>
            <a>Реферальная ссылка: <b>https://t.me/dollarluck_bot?start={{ user.referral_code }}</b></a>
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

p,
a,
b {
    user-select: all;
    /* Отключает выделение текста */
    -webkit-user-select: all;
    /* Для Safari */
    -moz-user-select: all;
    /* Для Firefox */
    -ms-user-select: all;
    /* Для IE */
    -webkit-touch-callout: all;
}
</style>