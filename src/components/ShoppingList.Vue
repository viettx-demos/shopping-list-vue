<template>
  <ul>
    <shopping-item
      v-for="item in list"
      :key="item.uid"
      :item="item"
      @delete="$emit('delete', item.uid)"
      @toogle="$emit('toogle', item.uid)"
    />
  </ul>
</template>

<script>
import ShoppingItem from '@/components/ShoppingItem'
export default {
  props: {
    list: Array
  },
  components: {
    ShoppingItem
  }
}
</script>

<style scoped>
  li {
    height: 80px;
  }
</style>
