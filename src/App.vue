<script setup>
import { onMounted } from 'vue';
import { RouterLink, RouterView } from 'vue-router'

onMounted(() => {
  if (window.Telegram && window.Telegram.WebApp) {
    const user = window.Telegram.WebApp.initDataUnsafe.user;
    if (user) {
      console.log("Пользователь:", user);
      this.user = user;
    } else {
      console.warn("Данные о пользователе недоступны");
    }
  } else {
    console.error("Telegram WebApp API недоступен");
  }
}) 
  



async function checkOrRegisterUser(user) {
    try {
        const response = await fetch("http://127.0.0.1:8000/api/user/", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(user),
        });

        const data = await response.json();
        console.log("Пользователь:", data);
        return data;
    } catch (error) {
        console.error("Ошибка:", error);
    }
}

// Пример данных от Telegram Web App
const telegramUser = {
    telegram_id: 123456789,
    first_name: "Иван",
    last_name: "Иванов",
    phone_number: "+998901234567",
};

onMounted(() => {
  checkOrRegisterUser(telegramUser);
})

</script>

<template>
  <RouterView />
</template>
