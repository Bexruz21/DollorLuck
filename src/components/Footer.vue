<script setup>

</script>

<template>
  <footer class="footer">
    <ul class="footer__list">
      <li class="footer__item">
        <RouterLink class="footer__link" to="/">
          <i class="fa-solid fa-ticket"></i>
          <p>Lotto</p>
        </RouterLink>
      </li>
      <li class="footer__item">
        <RouterLink class="footer__link" to="/">
          <i class="fa-solid fa-people-group"></i>
          <p>Ref</p>
        </RouterLink>
      </li>
      <li class="footer__item">
        <RouterLink class="footer__link" to="/">
          <i class="fa-solid fa-wallet"></i>
          <p>Wallet</p>
        </RouterLink>
      </li>
      <li class="footer__item">
        <RouterLink class="footer__link" to="/profile">
          <i class="fa-solid fa-user"></i>
          <p>Profile</p>
        </RouterLink>
      </li>
    </ul>
  </footer>
</template>

<style scoped>
a {
  -webkit-tap-highlight-color: transparent;
}
a:active {
  background-color: transparent;
}
.footer {
  width: 100%;
  height: 60px;
  background-color: #333;
  opacity: 20%;
  overflow: hidden;
}
.footer__list {
  width: 100%;
  height: 100%;
  list-style: none;
  margin: 0;
  padding: 0px 20px;
  display: flex;
  justify-content: space-around;
}
.footer__item {
  height: 100%;
  flex: 1;
  text-align: center;
  align-items: center;
}
.footer__link {
  height: 100%;
  color: #fff;
  text-decoration: none;
  padding: 10px;
  display: block;
  transition: 0.3s all;
  cursor: pointer;
}
.footer__item:hover {
  background-color: #9b0000;
}
</style>