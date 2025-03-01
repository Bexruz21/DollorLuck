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
    <template v-if="isOwner">
      <div class="admin">
        <h1>Choice your role</h1>
        <div class="admin__buttons">
          <button class="admin__button" role="button">Admin</button>
          <button class="admin__button" role="button">User</button>
        </div>
      </div>
    </template>
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

.admin {
  background: #000000;
  background: -webkit-linear-gradient(to right, #000000, #272727);
  background: linear-gradient(to right, #000000, #272727);
  min-height: 100vh;
  display: flex;
  gap: 10px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.admin__buttons {
  display: flex;
  flex-direction: column;
  gap: 10px;
  justify-content: center;
  align-items: center;
}


.admin__button {
  margin: 10px;
  width: 200px;
  padding: 15px 30px;
  text-align: center;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  border-radius: 2px;
  display: block;
  border: 0px;
  font-size: 16px;
  font-weight: 700;
  box-shadow: 0px 0px 14px -7px #f09819;
  background-image: linear-gradient(45deg, #FF512F 0%, #F09819 51%, #FF512F 100%);
  cursor: pointer;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.admin__button:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
}

.admin__button:active {
  transform: scale(0.95);
}

@keyframes l3 {
  to {
    transform: rotate(1turn)
  }
}
</style>
