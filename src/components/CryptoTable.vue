<template>
    <div class="crypto-container">
      <button @click="fetchCryptoData" class="get-data-btn">Get Data</button>
      <table v-if="cryptoData.length">
        <thead>
          <tr>
            <th>Name</th>
            <th>Symbol</th>
            <th>Harga USD</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="crypto in cryptoData" :key="crypto.id">
            <td>{{ crypto.name }}</td>
            <td>{{ crypto.symbol }}</td>
            <td>{{ crypto.price_usd }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref } from 'vue';
  import axios from 'axios';
  
  export default defineComponent({
    name: 'CryptoTable',
    setup() {
      const cryptoData = ref<any[]>([]);
  
      const fetchCryptoData = async () => {
        try {
          const response = await axios.get('https://api.coinlore.net/api/tickers/');
          cryptoData.value = response.data.data.map((item: any) => ({
            id: item.id,
            name: item.name,
            symbol: item.symbol,
            price_usd: item.price_usd,
          }));
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      };
  
      return {
        cryptoData,
        fetchCryptoData,
      };
    },
  });
  </script>
  
  <style scoped>
  .crypto-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .get-data-btn {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 20px;
    margin-bottom: 20px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .get-data-btn:hover {
    background-color: #0056b3;
  }
  
  table {
    border-collapse: collapse;
    width: 80%;
    text-align: left;
  }
  
  th, td {
    border: 1px solid #ddd;
    padding: 8px;
  }
  
  th {
    background-color: #f2f2f2;
  }
  </style>
  