<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = false
  
const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage },
  { id: 2235, color: 'blue', image: socksBlueImage },
])

const cart = ref(0)

const addToCart = () => {
  cart.value = cart.value + 1
}

const removeToCart = () => {
  if (cart.value > 0)
    cart.value = cart.value - 1
}

const changeImage = (imagePath) => {
  image.value = imagePath
}
</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-bind:src="image"
        :class="{'out-of-stock-img':!inStock}"
        >
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div
          v-for="variant in variants"
          :key="variant.id"
          class="color-circle"
          :style="{ backgroundColor: variant.color}"
          @mouseover="changeImage(variant.image)"
        >
        </div>
        <button 
        class="button" 
        :class="{disabledButton: !inStock}"
        :disabled="!inStock"
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