<template>
  <div class="products-list">
    <div class="product" v-for="product in store.products" :key="product.id">
      <img :src="product.thumbnail" alt="" />
      <h2>ブランド:{{ product.brand }}</h2>
      <p>詳細:{{ product.description }}</p>
      <p>価格:${{ product.price }}</p>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'CatalogView'
})
</script>

<script setup>
import { onMounted } from 'vue'
import { productsStore } from '@/stores/products'

const store = productsStore()

onMounted(() => {
  //   console.log('Mounted')
  store.fetchProductsFromDB()
})
</script>
