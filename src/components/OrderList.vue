<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    orders: Array,
    remark: String,
    totalPrice: Number
})
</script>

<template>
    <div class="col-8" v-if="!orders.length">
        <div class="alert alert-secondary text-center" role="alert">尚未建立訂單</div>
    </div>

    <div class="col-8" v-if="orders.length">
        <div class="card">
        <div class="card-body">
            <div class="card-title">
            <h5>訂單</h5>
            <table class="table">
                <thead>
                <tr>
                    <th scope="col">品項</th>
                    <th scope="col">數量</th>
                    <th scope="col">小計</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="order in orders" :key="order.id">
                    <td>{{ order.name }}</td>
                    <td>{{ order.num }}</td>
                    <td>{{ order.price*order.num }}</td>
                </tr>
                </tbody>
            </table>
            <div class="text-end">備註: <span>{{ remark?remark:'無' }}</span></div>
            <div class="text-end">
                <h5>總計: <span>{{ totalPrice }}</span></h5>
            </div>
            </div>
        </div>
        </div>
    </div>
</template>