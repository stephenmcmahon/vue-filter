<script setup>
  defineProps(['filterItem'])
  const emit = defineEmits(['expandBox']) // defining events to emit
  const handleClick = id => emit('expandBox', id) // emitting toggleDescription event with id attribute.
</script>

<template>
  <div :class="['filter-item', {open: filterItem.isOpen}]" @click="() => handleClick(filterItem.id)">
    <div>
      <h2>{{ filterItem.title }}</h2>
      <h3>{{ filterItem.brand }}</h3>
      <h4>${{ filterItem.regular_price.value }}</h4>
    </div>
    <div> 
      Add to cart
    </div>
  </div>
</template>

<style lang="less">

</style>