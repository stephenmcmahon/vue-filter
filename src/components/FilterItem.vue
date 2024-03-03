<script setup>
  import SvgIcon from './SvgIcon.vue'
  defineProps(['filterItem'])
  const emit = defineEmits(['expandBox']) // defining events to emit
  const handleClick = id => emit('expandBox', id) // emitting toggleDescription event with id attribute.
</script>

<template>
  <div :class="['filter-item', {open: filterItem.isOpen}]" @click="() => handleClick(filterItem.id)">
    <div :class="['description', {open: filterItem.isOpen}]">
      <h2>{{ item.title }}</h2>
      <h3>{{ item.brand }}</h3>
      <h4>${{ item.regular_price.value }}</h4>
    </div>
    <div :class="['add-btn', {open: filterItem.isOpen}]"> 
      Add to cart
    </div>
  </div>
</template>

<style lang="less">

</style>