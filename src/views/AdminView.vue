<script setup>
import Particles from '../components/Particles.vue';
</script>

<template>
    <div class="admin__container">
        <Particles />
        <div class="admin__form">
            <h1 class="admin__form-title">Login As</h1>
            <div class="admin__form-buttons">
                <button class="admin__form-button">Admin</button>
                <button class="admin__form-button">User</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.admin__container {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}
.admin__form {
  position: absolute;
  width: 80%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  z-index: 1;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  padding: 20px;
  border-radius: 5px;
}
.admin__form-title {
  margin-bottom: 20px;
}
.admin__form-buttons {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.admin__form-button {
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

.admin__form-button:hover {
  background-position: right center;
  color: #fff;
  text-decoration: none;
}
.admin__form-button:active {
  transform: scale(0.95);
}
</style>