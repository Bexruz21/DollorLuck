<script setup>
import { inject } from 'vue';

const user = inject("user");

const copyToClipboard = (ref_code) => {
    const inviteLink = `https://t.me/dollarluck_bot?start=${ref_code}`;
    navigator.clipboard.writeText(inviteLink)
};

</script>

<template>
    <div class="profile">
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
        <div class="invite-container">
            <div>
                <p class="invite-text">My invite link:</p>
                <p class="invite-link">https://t.me/dollarluck_bot?start={{ user.referral_code }}</p>
            </div>
            <button class="copy-button" @click="copyToClipboard(user.referral_code)">Copy</button>
        </div>
    </div>
</template>

<style scoped>
* {
    user-select: auto;
    -webkit-user-select: auto;
    -moz-user-select: auto;
    -ms-user-select: auto;
    -webkit-touch-callout: auto;
}

.profile {
    width: 100%;
    padding: 20px;
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