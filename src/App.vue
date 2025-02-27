<script setup>
import { onMounted, ref, provide } from 'vue';
import { RouterView } from 'vue-router';

const user = ref(null);
const user1 = ref(null)

onMounted(async () => {
  window.Telegram.WebApp.expand();
  if (window.Telegram?.WebApp) {
    const telegramUser = window.Telegram.WebApp.initDataUnsafe?.user;
    if (telegramUser) {
      user.value = await checkOrRegisterUser(telegramUser);
      user1.value = telegramUser
    }
  }
});

async function checkOrRegisterUser(user) {
    const BASE_URL = "https://5771-37-110-210-241.ngrok-free.app"

    const response = await fetch(`${BASE_URL}/api/user/`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        telegram_id: user.telegram_id,
        first_name: user.first_name,
        last_name: user.last_name || "",
        username: user.username || "",
      }),
    });
    let data = await response.json()
    return data
}

provide("user", user)
</script>

<template>
  <p>{{ user1.username }}</p>
  <p>{{ user1 }}</p>
  <RouterView />
</template>
