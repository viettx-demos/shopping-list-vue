<template>
  <div id="app">
    <h1>Shopping List</h1>
    <shopping-summary :summary="summary" @filter="onFilter" />
    <add-item @addItem="onAddItem" />
    <shopping-list :list="filteredItems" @toogle="onToogle" @delete="onDelete" />  
  </div>
</template>

<script>
import AddItem from '@/components/AddItem'
import ShoppingList from '@/components/ShoppingList'
import ShoppingSummary from '@/components/ShoppingSummary'
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
  computed: {
    summary () {
      const totalPrice = this.list.reduce((total, item) => total + item.quantity * item.price, 0)
      const countItemsLeft = this.list.filter(item => !item.completed).length
      const filter = this.filter

      return {
        totalPrice, countItemsLeft, filter
      }
    },

    filteredItems () {
      if (this.filter === 'all') {
        return this.list
      }

      return this.list.filter(item => !item.completed)
    }
  },
  methods: {
    onFilter (filter) {
      this.filter = filter
    },

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
    },

    onAddItem (item) {
      const newItem = {...item, uid: this.currentUID + 1, completed: false}
      this.list = [...this.list, newItem]
      this.currentUID += 1
    }
  },
  components: {
    ShoppingList,
    ShoppingSummary,
    AddItem
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
</style>
