<script setup>
import Footer from './components/Footer.vue'
import { onMounted, ref, provide } from 'vue';
import { RouterView, useRouter } from 'vue-router';

const user = ref(null);
const ref_code = ref(null)
const isLoaded = ref(false)
const router = useRouter()

onMounted(async () => {
  if (!window.location.hash || window.location.hash === "#/") {
    router.replace("/");
  }
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
  isLoaded.value = true
});

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
        ref_code: ref_code.value
      }),
    });
    let data = await response.json()
    return data
}

provide("user", user)

</script>

<template>
  <template v-if="isLoaded">
    <RouterView />
    <Footer />
  </template>
  <div class="loading" v-else>
    <h1>Loading...</h1>
  </div>
</template>

<style scoped>
.loading {
  background-color: black;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
