<script setup>
import { defineProps, defineEmits, ref } from 'vue';

const remark = ref('')
const emits = defineEmits(['handleOrders', 'clearProducts'])
const props = defineProps({
    products: Array,
    price: Number,
})

const deepCopy = (obj) => {
    return JSON.parse(JSON.stringify(obj));
}

const addOrder = () => {
  const orders = deepCopy(props.products) 
  const totalPrice = orders.reduce((sum, item) => sum + item.price*item.num,0)
  const showOrder = true
  
  emits('handleOrders', remark.value, showOrder, totalPrice, orders)
  emits('clearProducts')
  remark.value = ''
}

const deleteProduct = (item) => {
  const index = props.products.findIndex(product => product.id === item.id)
  props.products.splice(index, 1)
}

</script>

<template>

    <table class="table">
        <thead>
            <tr>
            <th scope="col" width="50">操作</th>
            <th scope="col">品項</th>
            <th scope="col">描述</th>
            <th scope="col" width="90">數量</th>
            <th scope="col">單價</th>
            <th scope="col">小計</th>
            </tr>
        </thead>
        <tbody v-if="products.length">
            <tr v-for="product in products" :key="product.id">
                <td><button type="button" class="btn btn-sm" @click="deleteProduct(product)">x</button></td>
                <td>{{ product.name }}</td>
                <td><small>{{ product.description }}</small></td>
                <td>
                    <select class="form-select" v-model="product.num">
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                    <option value="5">5</option>
                    <option value="6">6</option>
                    <option value="7">7</option>
                    <option value="8">8</option>
                    <option value="9">9</option>
                    <option value="10">10</option>
                    </select>
                </td>
                <td>{{ product.price }}</td>
                <td>{{ product.price * product.num }}</td>    
            </tr>
        </tbody>
    </table>
    <div class="alert alert-primary text-center" role="alert" v-if="!products.length">請選擇商品</div>
    <div class="text-end mb-3" v-if="products.length">
    <h5>總計: <span>{{ price }}</span></h5>
    </div>
    <textarea
    class="form-control mb-3"
    rows="3"
    placeholder="備註"
    v-if="products.length"
    v-model = "remark"
    ></textarea>
    <div class="text-end" v-if="products.length">
        <button class="btn btn-primary" @click="addOrder">送出</button>
    </div> 
</template>