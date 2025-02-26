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
.footer {
  width: 100%;
  background-color: #333;
  opacity: 20%;
}
.footer__list {
  width: 100%;
  list-style: none;
  margin: 0;
  padding: 0px 20px;
  display: flex;
  justify-content: space-around;
}
.footer__item {
  flex: 1;
  text-align: center;
  align-items: center;
  gap: 5px;
}
.footer__link {
  color: #fff;
  text-decoration: none;
  padding: 10px;
  display: block;
  transition: 0.3s all;
  cursor: pointer;
}
.footer__link:hover {
  background-color: #333;
}
</style>