<script setup>
import { onMounted, ref, provide } from 'vue';
import { RouterView } from 'vue-router';

const user = ref(null);

onMounted(async () => {
  window.Telegram.WebApp.expand();
  if (window.Telegram?.WebApp) {
    const telegramUser = window.Telegram.WebApp.initDataUnsafe?.user;
    if (!telegramUser) {
      user.value = await checkOrRegisterUser(telegramUser);
      provide("user", user); // Добавляем provide ПРАВИЛЬНО
    }
  }
});

async function checkOrRegisterUser(user) {
    const BASE_URL = "https://cbb0-195-158-2-216.ngrok-free.app"

    const response = await fetch(`${BASE_URL}/api/user/`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        telegram_id: 26420175325,
        username: "bekijan",
        first_name: "hudududu",
        last_name: "fhisdhfdsf" || "",
        username: "fdsfdsfdsf" || "",
      }),
    });
    console.log(response)
    return await response.json()
}
</script>

<template>
  <RouterView />
</template>
