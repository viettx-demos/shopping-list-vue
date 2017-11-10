<template>
  <div class="row add-new-item">
    <div class="form">
      <input v-model="formData.title" type="text" class="row item-name" placeholder="New item need to shop" />
      <div class="item-info">
        <input v-model="formData.price" type="text" class="row item-price" placeholder="Price" />
        <input v-model="formData.quantity" type="text" class="row item-quantity" placeholder="Quantity" />
        <input v-model="formData.unit" type="text" class="row item-unit" placeholder="Unit" />
      </div>
    </div>
    <button class="add-btn" @click="$emit('addItem', formData)">Add Item</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      formData: {
        title: '',
        price: '',
        quantity: '',
        unit: ''
      }
    }
  }
}
</script>

<style scoped>
  .add-new-item {
    height: 80px;
    display: flex;
    flex-direction: row;
  }

  .form {
    display: flex;
    flex-direction: column;
    flex: 1;
    margin-left: 15px;
  }

  input {
    font-size: 14px;
    padding: 5px 10px;
    outline: 0;
  }

  .item-name {
    width: 300px;
  }

  .item-quantity, 
  .item-price,
  .item-unit
  {
    width: 100px;
    margin-right: 5px;
  }

  .add-btn {
    padding: 5px 10px;
    margin-right: 15px;
  }

  .item-info {
    display: flex;
    flex-direction: row;
  }
</style>
