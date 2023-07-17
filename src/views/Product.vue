<template>
  <ProductDetail :product="currentProduct" v-if="currentProduct" />
  <PopularProducts />
  <AboutBrand />
  <Subscribe />
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import { useRoute } from 'vue-router'
import api from '@/api.js'
import ProductDetail from '@/components/ProductDetail.vue'
import AboutBrand from '@/components/AboutBrand.vue'
import Subscribe from '@/components/Subscribe.vue'
import PopularProducts from '@/components/PopularProducts.vue'

const route = useRoute()
const productId = ref('')
const currentProduct = ref({})

onMounted(async () => {
  productId.value = route.params.id
  currentProduct.value = await api.getProduct(productId.value)
})

watch(
  () => route.params.id,
  async (newProductId) => {
    productId.value = newProductId
    currentProduct.value = await api.getProduct(productId.value)
  }
)
</script>
