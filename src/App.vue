<script setup>
import { onMounted, ref } from 'vue';
import { RouterView } from 'vue-router';

const user = ref(null);

onMounted(async () => {
  if (window.Telegram?.WebApp) {
    const telegramUser = window.Telegram.WebApp.initDataUnsafe?.user;
    if (telegramUser) {
      user.value = telegramUser;
      await checkOrRegisterUser(telegramUser);
    }
  }
});

async function checkOrRegisterUser(user) {
    const BASE_URL = "https://b711-95-214-210-132.ngrok-free.app"
    const response = await fetch(`${BASE_URL}/api/user/`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        telegram_id: user.id,
        username: user.username,
        first_name: user.first_name,
        last_name: user.last_name || "",
        username: user.username || "",
      }),
    });
}
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

  <RouterView />
</template>

<style scoped>
h1 {
  color: white;
}
</style>

