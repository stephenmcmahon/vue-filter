<script setup>
  defineProps(['filterItem'])
</script>

<template>
  <div class="filter-item">
    <div class="product-info">
      <h2>{{ filterItem.title }}</h2>
      <h3>{{ filterItem.brand }}</h3>
      <h4>${{ filterItem.regular_price.value }}</h4>
    </div>
    <div class="cart-btn"> 
      Add to cart
    </div>
  </div>
</template>

<style lang="less">
  .filter-item {
    width: 200px;
    height: 200px;
    margin: 1rem;
    padding: 1rem;
    border-radius: 10px;
    background: #f8f8f8;
    box-shadow: 5px 5px 10px #dddddd, -5px -5px 10px #ffffff;
    transition: all 0.25s ease-in-out;
    cursor: pointer;
    &.active {
      transform: scale(1.5);
      z-index: 99;
      cursor: default;
    }
  }
</style>