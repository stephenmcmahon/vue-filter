<script setup>
  import { ref, computed } from 'vue'
  import FilterItem from './FilterItem.vue'
  const brand = ref([
    { id: 1, title: "Brand 1", sort: "100", code: "brand_1" },
    { id: 2, title: "Brand 2", sort: "200", code: "brand_2" }
  ])
  const items = ref([
    { type: "simple", id: 1, sku: "s1", title: "Product 1", regular_price: { currency: "USD", value: 27.12 }, image: "/images/1.png", brand: 1, isOpen: false },
    { type: "simple", id: 2, sku: "s1", title: "Product 2", regular_price: { currency: "USD", value: 37.88 }, image: "/images/1.png", brand: 2, isOpen: false },
    { type: "simple", id: 3, sku: "s1", title: "Product 3", regular_price: { currency: "USD", value: 39.77 }, image: "/images/1.png", brand: 2, isOpen: false }
  ])
  const filteredBrand = ref(null)
  const filteredItems = computed(() => {
    return filteredBrand.value ? items.value.filter(item => item.brand === filteredBrand.value) : items.value;
  })
  const filterByBrand = (brand = null) => {
    filteredBrand.value = brand;
  }
  const expandBox = id => {
    filteredItems.value = filteredItems.value.map(filterItem => filterItem.isOpen && filterItem.id !== id ? {...filterItem, isOpen: false} : filterItem)
    filteredItems.value = filteredItems.value.map(filterItem => filterItem.id === id ? {...filterItem, isOpen: !filterItem.isOpen} : filterItem)
  }
</script>

<template>
  <div id="filter">
    <div class="nav">
      <span class="#" @click="filterByBrand()"> All brands</span>
      <div class="#" v-for="(item, id) in brand" :key="id" @click="filterByBrand(item.id)">{{ item.title }}</div>
    </div>
    <div class="filter-wrap">
      <div class="filter-row">
        <FilterItem 
          v-for="filterItem in filteredItems"
          :key="filterItem.id"
          :filterItem="filterItem"
          @expand-box="expandBox"
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
 
<style scoped>

</style>