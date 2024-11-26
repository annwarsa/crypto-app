<template>
  <div id="app" class="app-container">
    <h1>Crypto Prices</h1>
    <CryptoTable />
  </div>
</template>

<script lang="ts">
import CryptoTable from './components/CryptoTable.vue';

export default {
  name: 'App',
  components: {
    CryptoTable,
  },
};
</script>

<style>
.app-container {
  font-family: Arial, sans-serif;
  text-align: center;
  margin-top: 20px;
}
</style>
