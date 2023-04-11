<script setup>
import { onMounted, ref } from 'vue';
import Currency from './components/Currency.vue';

const currencies = ref([]);

const query = ref('');

onMounted(() => {
  fetch('https://api.coinpaprika.com/v1/tickers').then(r => r.json()).then(d => {
      currencies.value = d.
      map(e => {
        return {
          id: e.id,
          name: e.name,
          price: e.quotes.USD.price,
          direction: e.quotes.USD.percent_change_30m > 0,
        };
      });
  });
});


</script>

<template>

  <div class="search-container">
    <input class="search" type="text" v-model="query">
  </div>

  <div class="currencies">
    <Currency v-for="currency in currencies.filter(e => e.name.toLowerCase().includes(query.toLowerCase()))" :currency="currency" />
  </div>
</template>

<style scoped>
  .currencies {
    display: flex;
    flex-wrap: wrap;
    justify-content: left;
    width: 1050px;
    margin: 0 auto;
  }

  .search-container {
    width: 200px;
    margin: 80px auto;
  }

  .search {
    padding: 10px;
    box-sizing: border-box;
    widows: 200px;
    font-size: 1.2rem;
  }
</style>
