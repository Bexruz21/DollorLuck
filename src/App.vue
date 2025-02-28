<script setup>
import Footer from './components/Footer.vue'
import { onMounted, ref, provide } from 'vue';
import { RouterView } from 'vue-router';

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
      user.value = await checkOrRegisterUser(telegramUser);
      if (user.id == 1173081114) {
        isOwner.value = true
      }
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
  <template v-if="!isOwner">
    <template v-if="isLoaded">
      <RouterView />
      <Footer />
    </template>
    <div class="loading" v-else>
      <span class="loader"></span>
    </div>
    <template v-else>
      <div class="admin">
        <h1>Choice your role</h1>
        <div class="admin__buttons">
          <button>Admin</button>
          <button>Gamer</button>
        </div>
      </div>
    </template>
  </template>
</template>

<style scoped>
.loading {
  background: #000000;
  background: -webkit-linear-gradient(to right, #000000, #272727);
  background: linear-gradient(to right, #000000, #272727);
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
  animation: l3 1s infinite linear;
}

@keyframes l3 {
  to {
    transform: rotate(1turn)
  }
}
</style>
