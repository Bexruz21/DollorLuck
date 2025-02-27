<script setup>
import { onMounted, ref, provide } from 'vue';
import { RouterView } from 'vue-router';
import axios from 'axios';

const user = ref(null);

onMounted(async () => {
  window.Telegram.WebApp.expand();
  if (window.Telegram?.WebApp) {
    const telegramUser = window.Telegram.WebApp.initDataUnsafe?.user;
    if (telegramUser) {
      user.value = await checkOrRegisterUser(telegramUser);
    }
  }
});

async function checkOrRegisterUser(telegramUser) {
    const BASE_URL = "https://cbb0-195-158-2-216.ngrok-free.app"
    const response = await axios.post(`${BASE_URL}/api/user/`, {
      telegram_id: telegramUser.id,
      username: telegramUser.username || "",
      first_name: telegramUser.first_name,
      last_name: telegramUser.last_name || "",
    });

    return response.data; // Возвращаем данные пользователя
}
provide("user", user);
</script>

<template>
  <RouterView />
</template>
