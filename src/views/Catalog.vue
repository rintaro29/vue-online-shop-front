<template>
  <div class="products-list">
    <div
      class="product"
      v-for="product in store.products"
      :key="product.id"
      @click="goToProductPage(product.id)"
    >
      <img :src="product.thumbnail" alt="" />
      <h2>ブランド:{{ product.brand }}</h2>
      <p>詳細:{{ product.description }}</p>
      <p>価格:${{ product.price }}</p>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import { useRouter } from 'vue-router'

export default defineComponent({
  name: 'CatalogView'
})
</script>

<script setup>
import { onMounted } from 'vue'
import { productsStore } from '@/stores/products'

const store = productsStore()
const router = useRouter()

const goToProductPage = (id) => {
  router.push({ name: 'ProductView', params: { id } })
}

onMounted(() => {
  //   console.log('Mounted')
  store.fetchProductsFromDB()
})
</script>

<style scoped>
.products-list {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}

.product {
  flex-basis: 28%;
  margin: 8px;
  padding: 16px;
  box-shadow: 0px 0px 14px 1px #e6e6e6;
  cursor: pointer;
}

.product img {
  width: 70%;
}
</style>
