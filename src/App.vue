<script setup>
import Footer from './components/Footer.vue'
import { onMounted, ref, provide } from 'vue';
import { RouterView } from 'vue-router';

const user = ref(null);
const ref_code = ref(null)

onMounted(async () => {
  window.Telegram.WebApp.expand();  
  if (window.Telegram?.WebApp) {
    const tg = window.Telegram.WebApp;
    const telegramUser = tg.initDataUnsafe?.user;
    const urlParams = new URLSearchParams(window.location.search);
    ref_code.value = urlParams.get("ref") || "null";

    if (telegramUser) {
      user.value = await checkOrRegisterUser(telegramUser);
    }
  }
});
alert(JSON.stringify(ref_code))
async function checkOrRegisterUser(user) {
    const BASE_URL = "https://b588-37-110-214-26.ngrok-free.app"

    const response = await fetch(`${BASE_URL}/api/user/`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        telegram_id: user.id,
        first_name: user.first_name,
        last_name: user.last_name || "",
        username: user.username || "",
        ref_code: ref_code
      }),
    });
    let data = await response.json()
    return data
}
provide("user", user)
</script>

<template>
  <p>{{ ref_code }}</p>
  <RouterView />
  <Footer />
</template>
