<script setup>
import { ref, computed } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const product = ref('Socks')
const brand = ref('CPNV')
  
const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage, quantity:10 },
  { id: 2235, color: 'blue', image: socksBlueImage, quantity:5 },
])

const cart = ref(0)

const selectedVariant = ref(0)

const addToCart = () => {
  cart.value = cart.value + 1
}

const removeToCart = () => {
  if (cart.value > 0)
    cart.value = cart.value - 1
}

const updateVariant = (index) => {
  selectedVariant.value = index
  console.log('Selected Variant Index:', index)
}
const fullTitle = computed(() => {
  return brand.value + ' ' + product.value 
})

const productImage = computed(() => {
  return variants.value[selectedVariant.value].image
})

const inStockStatus = computed(() => {
  return variants.value[selectedVariant.value].quantity > 0
})

</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-bind:src="productImage"
        :class="{'out-of-stock-img':!inStockStatus}"
        >
      </div>
      <div class="product-info">
        <h1>{{fullTitle}}</h1>
        <p v-if="inStockStatus">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          class="color-circle"
          :style="{ backgroundColor: variant.color}"
          @click="updateVariant(index)"
        >
        </div>
        <button 
        class="button" 
        :class="{disabledButton: !inStockStatus}"
        :disabled="!inStockStatus"
        @click="addToCart">Add to Cart</button>
        <button class="button" @click="removeToCart">Remove to Cart</button>
      </div>
    </div>
  </div>
</template>

<style>

.color-circle {
  width: 25px;
  height: 25px;
  border-radius: 50%;
  display: inline-block;
  margin-right: 8px;
  cursor: pointer;
  border: 1px solid #ccc;
}

.disabledButton {
  background-color: #d8d8d8;
  cursor: not-allowed;
}

.out-of-stock-img {
  opacity:0.5
}

</style>