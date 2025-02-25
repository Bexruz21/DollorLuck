<script setup>
import { onMounted, ref } from 'vue';
import { RouterView } from 'vue-router';

const user = ref(null); // Хранение данных пользователя

onMounted(async () => {
  if (window.Telegram?.WebApp) {
    const telegramUser = window.Telegram.WebApp.initDataUnsafe.user;
    if (telegramUser) {
      user.value = telegramUser; // Обновляем состояние
      await checkOrRegisterUser(telegramUser); // Отправляем на сервер
    } else {
      console.warn("Данные о пользователе недоступны");
    }
  } else {
    console.error("Telegram WebApp API недоступен");
  }
});

async function checkOrRegisterUser(user) {
  try {
    const response = await fetch("http://127.0.0.1:8000/api/user/", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        telegram_id: user.id,
        first_name: user.first_name,
        last_name: user.last_name || "",
        username: user.username || "",
      }),
    });

    const data = await response.json();
    console.log("Ответ сервера:", data);
  } catch (error) {
    console.error("Ошибка запроса:", error);
  }
}
</script>

<template>
  <div v-if="user">
    <h1>ID: {{ user.id }}</h1>
    <h2>Имя: {{ user.first_name }}</h2>
    <h3>Фамилия: {{ user.last_name || "Нет данных" }}</h3>
    <h3>Юзернейм: {{ user.username || "Нет данных" }}</h3>
  </div>
  <div v-else>
    <h1>Загрузка...</h1>
  </div>

  <RouterView />
</template>
