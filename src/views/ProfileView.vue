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
            <div class="invite-container">
                <div>
                    <p class="invite-text">My invite link:</p>
                    <p class="invite-link">https://t.me/dollarluck_bot?start={{ user.referral_code }} <span class="gift-icon"><i
                                class="fas fa-gift"></i></span></p>
                </div>
                <button class="copy-button">Copy</button>
            </div>
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

.invite-container {
    background-color: #2f2f5f;
    color: white;
    padding: 16px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    gap: 16px;
}

.invite-text {
    font-size: 1.125rem;
    font-weight: bold;
}

.gift-icon {
    color: #ffcc00;
}

.copy-button {
    background-color: #5a5a9f;
    color: white;
    font-weight: bold;
    padding: 8px 16px;
    border-radius: 12px;
    border: none;
    cursor: pointer;
}
</style>