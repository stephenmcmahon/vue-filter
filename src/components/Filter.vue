<script setup>
  import { ref, computed } from 'vue'
  import FilterItem from './FilterItem.vue'
  const brand = ref([
    { id: 1, title: "Nike", sort: "100", code: "brand_1" },
    { id: 2, title: "Adidas", sort: "200", code: "brand_2" },
    { id: 3, title: "Apple", sort: "300", code: "brand_3" },
    { id: 4, title: "Samsung", sort: "400", code: "brand_4" },
    { id: 5, title: "Google", sort: "500", code: "brand_5" },
    { id: 6, title: "Microsoft", sort: "600", code: "brand_6" }
  ])
  const items = ref([
    { type: "Nike", id: 1, sku: "s1", title: "Bluetooth-enabled smart water bottle", regular_price: { currency: "USD", value: 27.12 }, image: "product.jpg", brand: 1 },
    { type: "Adidas", id: 2, sku: "s1", title: "Bamboo cutting board set", regular_price: { currency: "USD", value: 37.88 }, image: "product.jpg", brand: 2 },
    { type: "Adidas", id: 3, sku: "s1", title: "Portable solar charger for electronic devices", regular_price: { currency: "USD", value: 39.77 }, image: "product.jpg", brand: 2 },
    { type: "Apple", id: 4, sku: "s1", title: "Resistance band set for home workouts", regular_price: { currency: "USD", value: 42.77 }, image: "product.jpg", brand: 3 },
    { type: "Apple", id: 5, sku: "s1", title: "Himalayan salt lamp", regular_price: { currency: "USD", value: 54.23 }, image: "product.jpg", brand: 3 },
    { type: "Apple", id: 6, sku: "s1", title: "Instant camera with film", regular_price: { currency: "USD", value: 60.99 }, image: "product.jpg", brand: 3 },
    { type: "Samsung", id: 7, sku: "s1", title: "Electric wine bottle opener", regular_price: { currency: "USD", value: 77.12 }, image: "product.jpg", brand: 4 },
    { type: "Samsung", id: 8, sku: "s1", title: "Silicone kitchen utensil set", regular_price: { currency: "USD", value: 87.88 }, image: "product.jpg", brand: 4 },
    { type: "Google", id: 9, sku: "s1", title: "Memory foam neck pillow for travel", regular_price: { currency: "USD", value: 99.77 }, image: "product.jpg", brand: 5 },
    { type: "Google", id: 10, sku: "s1", title: "Mini desktop vacuum cleaner", regular_price: { currency: "USD", value: 142.77 }, image: "product.jpg", brand: 5 },
    { type: "Microsoft", id: 11, sku: "s1", title: "Essential oil diffuser with LED lights", regular_price: { currency: "USD", value: 154.23 }, image: "product.jpg", brand: 6 },
    { type: "Microsoft", id: 12, sku: "s1", title: "Handheld milk frother for coffee beverages", regular_price: { currency: "USD", value: 260.99 }, image: "product.jpg", brand: 6 }
  ])
  const filteredBrand = ref(false)
  const filteredItems = computed(() => {
    return filteredBrand.value ? items.value.filter(item => item.brand === filteredBrand.value) : items.value
  })
  const filterByBrand = (brand = false) => {
    filteredBrand.value = brand
  }
  const isActive = ref(false)
  const toggleExpand = (el) => {
    if (isActive.value === el) {
      isActive.value = false
    } else {
      isActive.value = el
    }
  }
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
        color: var(--color-background);
        transition: all 0.25s ease-in-out;
        cursor: pointer;
        &:hover {
          color: var(--color-background-mute);
        }
      }
      .filter-btn {
        margin: 10px 0;
        padding: 5px;
        border-radius: 8px;
        background: linear-gradient(145deg, #ffffff, #aaaaaa);
        transition: all 0.25s ease-in-out;
        cursor: pointer;
        &:hover {
          background: linear-gradient(145deg, #ececec, #ffffff);
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