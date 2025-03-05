<script setup>
import { onMounted, ref, provide } from 'vue';
import AdminView from './views/AdminView.vue';
import Footer from './components/Footer.vue';

const user = ref(null);
const ref_code = ref(null)
const isLoaded = ref(false)
const isOwner = ref(false)

onMounted(async () => {
  window.Telegram.WebApp.expand();
  if (window.Telegram?.WebApp) {
    const tg = window.Telegram.WebApp;
    const telegramUser = tg.initDataUnsafe?.user;
    const urlParams = new URLSearchParams(window.location.search);
    ref_code.value = urlParams.get("ref") || "null";

    if (telegramUser) {
      if (String(telegramUser.id) === "1173081114") {
        setTimeout(() => {
          isOwner.value = true
          isLoaded.value = true
        }, 5000)
      }
    }
  }

  user.value = await checkOrRegisterUser(telegramUser);
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
    <AdminView v-if="isOwner" />
    <template v-else>
      <RouterView />
      <Footer />
    </template>
  </template>
  <template v-else>
    <div class="loading">
      <div class="loader"></div>
    </div>
  </template>
</template>


<style scoped>
.loading {
  background-color: #000000;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.loader {
  width: 50px;
  padding: 8px;
  aspect-ratio: 1;
  border-radius: 50%;
  background: #ffffff;
  --_m:
    conic-gradient(#0000 10%, #000),
    linear-gradient(#000 0 0) content-box;
  -webkit-mask: var(--_m);
  mask: var(--_m);
  -webkit-mask-composite: source-out;
  mask-composite: subtract;
  animation: loader 1s infinite linear;
}

@keyframes loader {
  to {
    transform: rotate(1turn)
  }
}
</style>
