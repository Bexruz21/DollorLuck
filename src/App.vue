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
          <button class="button-87" role="button">Admin</button>
          <button class="button-36" role="button">Gamer</button>
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


.button-87 {
  margin: 10px;
  width: 200px;
  padding: 15px 30px;
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  border-radius: 10px;
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

.button-87:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
}

.button-87:active {
  transform: scale(0.95);
}

/* CSS */
.button-36 {
  background-image: linear-gradient(92.88deg, #455EB5 9.16%, #5643CC 43.89%, #673FD7 64.72%);
  border-radius: 8px;
  border-style: none;
  box-sizing: border-box;
  width: 200px;
  color: #FFFFFF;
  cursor: pointer;
  flex-shrink: 0;
  font-family: "Inter UI","SF Pro Display",-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Oxygen,Ubuntu,Cantarell,"Open Sans","Helvetica Neue",sans-serif;
  font-size: 16px;
  font-weight: 500;
  height: 4rem;
  padding: 15px 30px;
  text-align: center;
  text-shadow: rgba(0, 0, 0, 0.25) 0 3px 8px;
  transition: all .5s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-36:hover {
  box-shadow: rgba(80, 63, 205, 0.5) 0 1px 30px;
  transition-duration: .1s;
}

@media (min-width: 768px) {
  .button-36 {
    padding: 0 2.6rem;
  }
}

@keyframes l3 {
  to {
    transform: rotate(1turn)
  }
}
</style>
