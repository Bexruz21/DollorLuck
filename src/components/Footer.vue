<script setup>

</script>

<template>
    <footer class="footer">
        <ul class="footer__list">
            <li class="footer__item">
                <a class="footer__link">Ref</a>
            </li>
            <li class="footer__item">
                <a class="footer__link">Lotto</a>
            </li>
            <li class="footer__item">
                <a class="footer__link">Leaders</a>
            </li>
            <li class="footer__item">
                <a class="footer__link">Profile</a>
            </li>
        </ul>
    </footer>
</template>

<style scoped>
    .footer {
        width: 100%;
        padding: 10px 0px;
    }
    .footer__list {
        margin: 0;
        padding: 0px 20px;
        display: flex;
        justify-content: space-around;
    }
    .footer {
  background-color: #333;
  padding: 10px 0;
}

.footer__nav {
  display: flex;
  justify-content: space-around;
}

.footer__list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  width: 100%;
  justify-content: space-around;
}

.footer__item {
  flex: 1;
  text-align: center;
}

.footer__link {
  color: #fff;
  text-decoration: none;
  padding: 10px;
  display: block;
  transition: 0.3s all;
  cursor: pointer;
  &:hover {
    background-color: red;
  }
}

.footer__link--active {
  background-color: #555;
}
</style>