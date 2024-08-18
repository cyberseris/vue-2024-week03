<script setup>
import { ref, watch } from 'vue';
import MenuList from './components/MenuList.vue';
import ProductList from './components/ProductList.vue';
import OrderList from './components/OrderList.vue';

const products = ref([])
const orders = ref([])
const price = ref(0)
const remark = ref('')
const showOrder = ref(false)
const totalPrice = ref(0)

const handleOrders = (pdRemark, pdShowOrder, pdTotalPrice, pdOrders) => {
  remark.value = pdRemark
  showOrder.value = pdShowOrder
  totalPrice.value = pdTotalPrice
  orders.value = pdOrders
}

const clearProducts = () => {
  products.value = []
}

watch(
  products,
  (newProducts)=>{
    price.value = newProducts.reduce((sum, item) => sum + item.price*item.num,0)
  },
  {deep:true}
)

</script>

<template>
  <div>
    <div class="container mt-5">
      <div class="row">
        <div class="col-md-4">
          <MenuList 
          :products="products" 
          />
        </div>

        <div class="col-md-8">
          <ProductList 
          :products="products" 
          :price="price" 
          @handleOrders="handleOrders"
          @clearProducts="clearProducts"
          />
        </div>
      </div>

      <hr />

      <div class="row justify-content-center mb-3" >
        <OrderList 
        :orders="orders" 
        :remark="remark" 
        :totalPrice="totalPrice" />
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
