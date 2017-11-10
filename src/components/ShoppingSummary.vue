<template>
  <div class="row shopping-summary">
    <span class="item-left">{{summary.countItemsLeft}} items left</span>
    <ul class="filters">
      <li :class="{actived: summary.filter === 'all'}" @click="$emit('filter', 'all')">All</li>
      <li :class="{actived: summary.filter === 'incomplete'}" @click="$emit('filter', 'incomplete')">Incomplete</li>
    </ul>
    <span class="total">Total: ${{summary.totalPrice}}</span>
  </div>
</template>

<script>
export default {
  props: {
    summary: Object
  },
  computed: {
    filters () {
      return ['All', 'Incomplete']
    }
  }
}
</script>

<style scoped>
  .shopping-summary {
    height: 50px;
    padding: 0 20px;
    background-color: #757575;
    color: #FAFAFA;
    font-size: 14px;
    font-weight: 400;
  }

  .filters {
    flex: 2;
  }

  .filters li {
    display: inline-block;
    padding: 5px 10px;
    border-radius: 10px;
    margin: 0 5px;
    cursor: pointer;
    border: 1px solid transparent;
  }

  .filters li:hover, .filters li.actived {
    border: 1px solid #E0E0E0;
  }

  .item-left {
    flex: 1;
  }

  .total {
    width: 105px;
    text-align: right;
    font-size: 16px;
  }
</style>
