<template>
  <button @click="router.push({ name: 'Catalog' })">カタログへ戻る</button>

  <div v-if="!store.cart.length" style="text-align: center">
    <p>カートは空です</p>
  </div>
  <div class="cart-items">
    <div class="cart-item" v-for="item in store.cart" :key="item.id">
      <div class="item-details">
        <img :src="item.thumbnail" alt="" />
        <span>ブランド: {{ item.brand }}</span>
        <span>カテゴリー: {{ item.category }}</span>
        <span>価格: {{ item.price }}</span>
        <button @click="removeFromCart(item.id)">削除</button>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'CartView'
})
</script>

<script setup>
import { productsStore } from '@/stores/products'

import { useRouter } from 'vue-router'
const router = useRouter()
const store = productsStore()

const removeFromCart = (id) => {
  store.removeFromCart(id)
}
</script>

<style scoped>
.item-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  box-shadow: 0 0 17px 6px #e7e7e7;
  border-radius: 8px;
  padding: 16px;
}

.item-detail {
  widows: 20%;
}
</style>
