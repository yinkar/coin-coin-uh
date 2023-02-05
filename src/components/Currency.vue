<script setup>
defineProps({
  currency: Object,
});
</script>

<template>
  <div>
    <div>
      <strong>
        {{ currency.name }}
      </strong>
    </div>
    <div class="price-area">
      <div class="price">
        {{ new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(currency.price) }}
      </div>
      <div class="direction" :class="{ up: currency?.direction, down: !currency?.direction }">
        {{ currency.direction ? '⬆' : '⬇' }}
      </div>
    </div>
  </div>
</template>

<style scoped>
  .price-area {
    display: flex;
  }

  .direction {
    line-height: 1.3rem;
  }

  .up {
    color: greenyellow;
  }

  .down {
    color: crimson;
  }
</style>
