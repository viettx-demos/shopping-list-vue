<template>
  <div id="app">
    <h1>Shopping List</h1>
    <div class="row shopping-summary">
      <span class="item-left">3 items left</span>
      <ul class="filters">
        <li class="actived">All</li>
        <li>Incomplete</li>
      </ul>
      <span class="total">Total: $2,065</span>
    </div>

    <div class="row add-new-item">
      <div class="form">
        <input type="text" class="row item-name" placeholder="New item need to shop" />
        <div class="item-info">
          <input type="text" class="row item-price" placeholder="Price" />
          <input type="text" class="row item-quantity" placeholder="Quantity" />
          <input type="text" class="row item-unit" placeholder="Unit" />
        </div>
      </div>
      <button class="add-btn">Add Item</button>
    </div>
    <shopping-list :list="list" @toogle="onToogle" @delete="onDelete" />  
  </div>
</template>

<script>
import ShoppingList from '@/components/ShoppingList'
export default {
  name: 'app',
  data () {
    return {
      list: [
        {
          uid: 1,
          title: 'Iphone X',
          price: 1000,
          quantity: 2,
          unit: 'device',
          completed: false
        },
        {
          uid: 2,
          title: 'Apple',
          price: 5,
          quantity: 10,
          unit: 'kg',
          completed: false
        },
        {
          uid: 3,
          title: 'Coca-Cola',
          price: 3,
          quantity: 5,
          unit: 'bottle',
          completed: false
        }
      ],
      filter: 'all',
      currentUID: 3
    }
  },
  methods: {
    onToogle (uid) {
      for (let item of this.list) {
        if (item.uid === uid) {
          item.completed = !item.completed
          break
        }
      }
    },
    onDelete (uid) {
      this.list = this.list.filter(item => item.uid !== uid)
    }
  },
  components: {
    ShoppingList
  }
}
</script>

<style>
h1, h2, h3, h4, h5 { margin: 0; }

body {
	font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
	line-height: 1.4em;
	background: #fff;
	color: #333333;
	min-width: 320px;
	max-width: 550px;
	margin: 10px auto;
	font-weight: 300;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	-webkit-text-rendering: optimizeLegibility;
	-moz-text-rendering: optimizeLegibility;
	text-rendering: optimizeLegibility;
}

ul {
	list-style: none;
	margin: 0;
	padding: 0;
}

li {
	margin: 0;
	padding: 0;
}

h1 {
  font-size: 65px;
	font-weight: 200;
	text-align: center;
	color: #616161;
	margin: 60px 0;
}

h2 {
	font-size: 20px;
	font-weight: 400;
}

.row {
	border: 1px solid #E0E0E0;
	border-radius: 10px;
	display: flex;
	flex-direction: row;
	align-items: center;
	margin: 5px 0;
}

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
	/* background-color: #F5F5F5;
	color: #616161; */
}

.shopping-summary .item-left {
	flex: 1;
}
.shopping-summary .total {
	width: 105px;
	text-align: right;
	font-size: 16px;
}

.add-new-item {
	height: 80px;
	display: flex;
	flex-direction: row;
}

.add-new-item .form {
	display: flex;
	flex-direction: column;
	flex: 1;
	margin-left: 15px;
}

.add-new-item .form input {
	font-size: 14px;
	padding: 5px 10px;
	outline: 0;
}

.add-new-item .form .item-name {
	width: 300px;
}

.form .item-quantity, 
.form .item-price,
.form .item-unit
{
	width: 100px;
	margin-right: 5px;
}

.add-new-item .add-btn {
	padding: 5px 10px;
	margin-right: 15px;
}

.add-new-item .form .item-info {
	display: flex;
	flex-direction: row;
}

.shopping-list li {
	height: 80px;
}

.shopping-list li .icon {
	margin: 0 10px;
}

.shopping-list li .toogle {
	text-align: center;
	width: 40px;
	height: 40px;
	border: none; /* Mobile Safari */
	margin: 0 10px;
	-webkit-appearance: none;
	appearance: none;
}

.shopping-list li .toogle:focus {
	outline: 0;
}

.shopping-list li .toogle:after {
	content: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="-10 -18 100 135"><circle cx="50" cy="50" r="50" fill="none" stroke="#BDBDBD" stroke-width="3"/></svg>');
}

.shopping-list li .toogle:checked:after {
	content: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="-10 -18 100 135"><circle cx="50" cy="50" r="50" fill="none" stroke="#bddad5" stroke-width="3"/><path fill="#5dc2af" d="M72 25L42 71 27 56l-4 4 20 20 34-52z"/></svg>');
}

.shopping-list li .info {
	flex: 1;
	line-height: 1.6em;
}

.shopping-list li .sub-info {
	font-size: 16px;
	display: flex;
	flex-direction: row;
	width: 230px;
}

.shopping-list li .quantity {
	width: 140px;
	display: inline-block;
}

.shopping-list li .sub-total {
	font-size: 17px;
	font-weight: 400;
	margin-right: 15px;
}

.shopping-list li .delete {
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

.shopping-list li .delete:hover {
	color: #af5b5e;
}
</style>
