<script setup>
defineProps({
  currency: Object,
});
</script>

<template>
  <div class="currency">
    <div>
      <strong>
        {{ currency.name }}
      </strong>
    </div>
    <div class="price-area">
      <div class="direction" :class="{ up: currency?.direction, down: !currency?.direction }">
        {{ currency.direction ? '⬆' : '⬇' }}
      </div>
      <div class="price">
        {{ new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(currency.price) }}
      </div>
    </div>
  </div>
</template>

<style scoped>
  .currency {
    padding: 10px 20px;
    margin: 30px 20px;
    width: 180px;
    border: 1px solid #444;
    border-radius: 10px;
    background-color: #333;
    box-shadow: 0px 5px 10px rgba(0, 0, 0, .3);
  }

  .currency strong {
    margin-bottom: 10px;
    display: block;
    line-height: 20px;
  }

  .price-area {
    display: flex;
  }

  .direction {
    line-height: 1.3rem;
    margin-right: 3px;
  }

  .up {
    color: greenyellow;
  }

  .down {
    color: crimson;
  }
</style>
