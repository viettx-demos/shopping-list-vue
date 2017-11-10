<template>
  <li class="row">
    <input type="checkbox" class="toogle" :checked="item.completed" v-on:change="$emit('toogle')" />
    <div class="info">
      <h2>{{item.title}}</h2>
      <div class="sub-info">
        <span class="quantity">Quantity: {{item.quantity}}</span>
        <span>${{item.price}}/{{item.unit}}</span>
      </div>
    </div>
    <span class="sub-total">${{subTotal}}</span>
    <a class="delete" @click="$emit('delete')">x</a>
  </li>
</template>

<script>
export default {
  props: {
    item: Object
  },
  computed: {
    subTotal () {
      return this.item.quantity * this.item.price
    }
  }
}
</script>

<style scoped>
  .icon {
    margin: 0 10px;
  }

  .toogle {
    text-align: center;
    width: 40px;
    height: 40px;
    border: none; /* Mobile Safari */
    margin: 0 10px;
    -webkit-appearance: none;
    appearance: none;
  }

  .toogle:focus {
    outline: 0;
  }

  .toogle:after {
    content: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="-10 -18 100 135"><circle cx="50" cy="50" r="50" fill="none" stroke="#BDBDBD" stroke-width="3"/></svg>');
  }

  .toogle:checked:after {
    content: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="-10 -18 100 135"><circle cx="50" cy="50" r="50" fill="none" stroke="#bddad5" stroke-width="3"/><path fill="#5dc2af" d="M72 25L42 71 27 56l-4 4 20 20 34-52z"/></svg>');
  }

  .info {
    flex: 1;
    line-height: 1.6em;
  }

  .sub-info {
    font-size: 16px;
    display: flex;
    flex-direction: row;
    width: 230px;
  }

  .quantity {
    width: 140px;
    display: inline-block;
  }

  .sub-total {
    font-size: 17px;
    font-weight: 400;
    margin-right: 15px;
  }

  .delete {
    width: 20px;
    height: 23px;
    background: none;
    border: 0;
    display: block;
    font-size: 20px;
    color: #424242;
    cursor: pointer;
    outline: 0;
  }

  .delete:hover {
    color: #af5b5e;
  }
</style>
