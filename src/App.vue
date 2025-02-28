<script setup>
import Footer from './components/Footer.vue'
import { onMounted, ref, provide } from 'vue';
import { RouterView } from 'vue-router';

const user = ref(null);
const refCode = ref(null)
const code = ref(null)

onMounted(async () => {
  window.Telegram.WebApp.expand();  
  if (window.Telegram?.WebApp) {
    const tg = window.Telegram.WebApp;
    const telegramUser = tg.initDataUnsafe?.user;

    const urlParams = new URLSearchParams(window.location.search);
    code.value = urlParams.get("ref") || "null";

    if (telegramUser) {
      user.value = await checkOrRegisterUser(telegramUser);
      refCode.value = tg.initDataUnsafe?.start_param;
      alert(JSON.stringify(refCode))
    }
  }
});
alert(JSON.stringify(refCode[0]))
alert(JSON.stringify(refCode))
alert(refCode)

async function checkOrRegisterUser(user) {
    const BASE_URL = "https://0ff5-95-214-211-48.ngrok-free.app"

    const response = await fetch(`${BASE_URL}/api/user/`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        telegram_id: user.id,
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
  <p>{{ refCode }}</p>
  <p>{{ code }}</p>
  <RouterView />
  <Footer />
</template>
