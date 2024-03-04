<script setup>
  import { ref, computed } from 'vue'
  import FilterItem from './FilterItem.vue'
  const brand = ref([
    { id: 1, title: "Brand 1", sort: "100", code: "brand_1" },
    { id: 2, title: "Brand 2", sort: "200", code: "brand_2" },
    { id: 3, title: "Brand 3", sort: "300", code: "brand_3" }
  ])
  const items = ref([
    { type: "simple", id: 1, sku: "s1", title: "Product 1", regular_price: { currency: "USD", value: 27.12 }, image: "/images/1.png", brand: 1 },
    { type: "simple", id: 2, sku: "s1", title: "Product 2", regular_price: { currency: "USD", value: 37.88 }, image: "/images/1.png", brand: 2 },
    { type: "simple", id: 3, sku: "s1", title: "Product 3", regular_price: { currency: "USD", value: 39.77 }, image: "/images/1.png", brand: 2 },
    { type: "simple", id: 4, sku: "s1", title: "Product 4", regular_price: { currency: "USD", value: 42.77 }, image: "/images/1.png", brand: 3 },
    { type: "simple", id: 5, sku: "s1", title: "Product 5", regular_price: { currency: "USD", value: 54.23 }, image: "/images/1.png", brand: 3 },
    { type: "simple", id: 6, sku: "s1", title: "Product 6", regular_price: { currency: "USD", value: 60.99 }, image: "/images/1.png", brand: 3 }
  ])
  const filteredBrand = ref(null)
  const filteredItems = computed(() => {
    return filteredBrand.value ? items.value.filter(item => item.brand === filteredBrand.value) : items.value
  })
  const filterByBrand = (brand = null) => {
    filteredBrand.value = brand
  }
  const isActive = ref(false)
  const toggleExpand = (el) => {
    isActive.value = el
  }
  // const expandBox = id => {
  //   filteredItems.value = filteredItems.value.map(filterItem => filterItem.isOpen && filterItem.id !== id ? {...filterItem, isOpen: false} : filterItem)
  //   filteredItems.value = filteredItems.value.map(filterItem => filterItem.id === id ? {...filterItem, isOpen: !filterItem.isOpen} : filterItem)
  // }
</script>

<template>
  <div id="filter">
    <div class="nav">
      <span @click="filterByBrand()"> All brands</span>
      <div class="filter-btn" v-for="(item, id) in brand" :key="id" @click="filterByBrand(item.id)">{{ item.title }}</div>
    </div>
    <div class="products-wrap">
      <div class="products-row">
        <FilterItem 
          v-for="filterItem in filteredItems"
          :key="filterItem.id"
          :filterItem="filterItem"
          @click="toggleExpand(filterItem.id)"
          :class="{ active : isActive == filterItem.id }"
        />
        <!-- <div v-for="(item, id) in filteredItems" :key="id">
          {{ item.title }} brand {{ item.brand }} ${{ item.regular_price.value }}
          <div id="btn"> 
            Add to cart
          </div>
        </div> -->
      </div>
    </div>
  </div>
</template>
 
<style scoped lang="less">
  #filter {
    display: flex;
    flex-wrap: nowrap;
    .nav {
      width: 25%;
      padding: 2rem;
      text-align: center;
      span {
        color: var(--color-heading);
        transition: all 0.25s ease-in-out;
        cursor: pointer;
        &:hover {
          color: var(--color-text);
        }
      }
      .filter-btn {
        margin: 10px 0;
        padding: 10px;
        border-radius: 8px;
        background: linear-gradient(145deg, #ffffff, #dfdfdf);
        box-shadow: 4px 4px 2px #c1c1c1, -4px -4px 2px #ffffff;
        transition: all 0.25s ease-in-out;
        cursor: pointer;
        &:hover {
          box-shadow: -5px -5px 10px #ffffff;
        }
      }
    }
    .products-wrap {
      width: 75%;
      padding: 2rem;
      .products-row {
        display: flex;
        flex-wrap: wrap;
      }
    }
  }
</style>