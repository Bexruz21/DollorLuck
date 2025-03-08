<template>
    <div class="wallet-container">
      <button @click="connectWallet">
        {{ walletAddress ? `Подключено: ${shortAddress(walletAddress)}` : "Подключить Wallet" }}
      </button>
  
      <div v-if="walletAddress" class="wallet-info">
        <p>Адрес: {{ walletAddress }}</p>
        <p>Баланс USDT: {{ usdtBalance }} USDT</p>
        <button @click="checkBalance">Обновить баланс</button>
      </div>
    </div>
  </template>
  
  <script>
  import { TonConnect } from "@tonconnect/sdk";
  
  export default {
    data() {
      return {
        tonConnect: null,
        walletAddress: null,
        usdtBalance: 0
      };
    },
    async mounted() {
      this.tonConnect = new TonConnect({
        manifestUrl: "https://dollor-luck.vercel.app/tonconnect-manifest.json"
      });
  
      // Проверяем, подключен ли кошелек
      const wallet = this.tonConnect.account;
      if (wallet) {
        this.walletAddress = wallet.address;
        await this.checkBalance();
      }
    },
    methods: {
      async connectWallet() {
        try {
          await this.tonConnect.connect();
          const wallet = this.tonConnect.account;
          if (wallet) {
            this.walletAddress = wallet.address;
            await this.checkBalance();
          }
        } catch (error) {
          console.error("Ошибка подключения:", error);
        }
      },
      async checkBalance() {
        if (!this.walletAddress) return;
  
        try {
          const response = await fetch(`https://tonapi.io/v1/blockchain/account/${this.walletAddress}`);
          const data = await response.json();
          this.usdtBalance = data.tokens?.USDT || 0;
        } catch (error) {
          console.error("Ошибка получения баланса:", error);
        }
      },
      shortAddress(address) {
        return `${address.slice(0, 5)}...${address.slice(-5)}`;
      }
    }
  };
  </script>
  
  <style scoped>
  .wallet-container {
    text-align: center;
    margin-top: 20px;
  }
  button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
  }
  .wallet-info {
    margin-top: 10px;
  }
  </style>
  