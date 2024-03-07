<script setup>
  defineProps(['filterItem'])
</script>

<template>
  <div class="filter-item">
    <div class="product-info">
      <div class="product-title">{{ filterItem.title }}</div>
      <div class="product-brand">{{ filterItem.brand }}</div>
      <img alt="Product Image" src="../assets/product.jpg" />
      <div class="product-price">${{ filterItem.regular_price.value }}</div>
    </div>
    <div class="cart-btn"> 
      Add to cart
    </div>
  </div>
</template>

<style lang="less">
  .filter-item {
    width: 200px;
    min-width: 200px;
    min-height: 200px;
    margin: 1rem;
    padding: 1rem;
    border-radius: 10px;
    background: #f8f8f8;
    box-shadow: 5px 5px 10px #dddddd, -5px -5px 10px #ffffff;
    transition: all 0.25s ease-in-out;
    animation-name: fade;
    animation-duration: 1s;
    cursor: pointer;
    &.active {
      transform: scale(1.5);
      z-index: 99;
      cursor: default;
      .cart-btn {
        opacity: 1;
      }
    }
    .product-info {
      img {
        width: 75px;
        margin: 0 auto;
      }
    }
    .cart-btn {
      opacity: 0;
      transition: all 0.25s ease-in-out;
      cursor: pointer;
    }
  }

  @keyframes fade {
    from {opacity: 0;}
    to {opacity: 1;}
  }
</style>