<script setup>
  defineProps(['filterItem'])
</script>

<template>
  <div class="filter-item">
    <div class="product-info">
      <div class="product-title">{{ filterItem.title }}</div>
      <div class="product-brand">{{ filterItem.type }}</div>
      <img alt="Product Image" :src="'/src/assets/' + filterItem.image" />
      <div class="product-price">${{ filterItem.regular_price.value }}</div>
    </div>
    <div class="cart-btn"> 
      Add to cart
    </div>
  </div>
</template>

<style lang="less">
  .filter-item {
    position: relative;
    width: 200px;
    min-width: 200px;
    min-height: 200px;
    max-height: 200px;
    margin: 1rem;
    padding: 1rem;
    border-radius: 10px;
    background: #f8f8f8;
    transition: all 0.25s ease-in-out;
    animation-name: fade;
    animation-duration: 1s;
    cursor: pointer;
    &.active {
      transform: scale(1.75);
      z-index: 99;
      box-shadow: 5px 5px 10px rgba(0,0,0,0.25), -5px -5px 10px rgba(0,0,0,0.25);
      cursor: default;
      .cart-btn {
        opacity: 1;
      }
    }
    .product-info {
      width: auto;
      .product-title {
        font-size: 14px;
        font-weight: bold;
        line-height: 14px;
      }
      .product-brand {
        font-size: 12px;
      }
      img {
        width: 80px;
        margin: auto;
        display: block;
      }
      .product-price {
        font-weight: bold;
        font-size: 18px;
        text-align: center;

      }
    }
    .cart-btn {
      opacity: 0;
      position: absolute;
      bottom: 3px;
      left: 50%;
      transform: translate(-50%, 0);
      width: 65%;
      text-align: center;
      background-color: var(--color-heading);
      font-size: 12px;
      text-transform: uppercase;
      font-weight: bold;
      color: var(--color-background);
      border-radius: 8px;
      transition: all 0.25s ease-in-out;
      cursor: pointer;
    }
  }

  @keyframes fade {
    from {opacity: 0;}
    to {opacity: 1;}
  }
</style>