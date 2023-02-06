<script setup>
import { onMounted, ref } from 'vue';
import Currency from './components/Currency.vue';

const currencies = ref([]);

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
  <div class="currencies">
    <Currency v-for="currency in currencies" :currency="currency" />
  </div>
</template>

<style scoped>
  .currencies {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
</style>
