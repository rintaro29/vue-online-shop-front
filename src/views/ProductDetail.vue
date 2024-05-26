<template>
  <button @click="router.push({ name: 'Catalog' })">カタログへ戻る</button>
  <div class="product">
    <div class="product-image">
      <img :src="selectedProduct.thumbnail" alt="" />
    </div>
    <div class="product-details">
      <p>ブランド: {{ selectedProduct.brand }}</p>
      <p>詳細: {{ selectedProduct.description }}</p>
      <h2>価格: {{ selectedProduct.price }}</h2>
      <button @click="addToCart">Add to cart</button>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ProductDetail'
})
</script>

<script setup>
import { computed } from 'vue'
import { productsStore } from '@/stores/products'
import { useRoute, useRouter } from 'vue-router'

const store = productsStore()
const route = useRoute()
const router = useRouter()

const selectedProduct = computed(() => {
  return store.products.find((item) => item.id === parseInt(route.params.id))
})
const addToCart = () => {
  store.addToCart(selectedProduct.value)
  router.push({ name: 'CartView' })
}
</script>

<style scoped>
.product {
  display: flex;
  margin-top: 50px;
}

.product-image {
  margin-right: 24px;
}
</style>
