<script setup>
import { ref, computed } from 'vue'
const props = defineProps({
  premium: {
    type: Boolean,
    required: true
  }
})

import socksGreenImage from '../assets/images/socks_green.jpeg'
import socksBlueImage from '../assets/images/socks_blue.jpeg'

const product = ref('Socks')
const brand = ref('Vue Mastery')

const image = ref(socksGreenImage)
const inStock = ref(false)

const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage },
  { id: 2235, color: 'blue', image: socksBlueImage },
])

const updateImage = (variantImage) => image.value = variantImage

const shipping = computed(() => {
  if (props.premium) {
    return 'Gratuit'
  }
  return '5.99 CHF'
})

const addToCart = () => {}
const removeToCart = () => {}
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="image">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>

        <p>Frais de Port: {{ shipping }}</p>

        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div
            v-for="variant in variants"
            :key="variant.id"
            @mouseover="updateImage(variant.image)"
            class="color-circle"
            :style="{ backgroundColor: variant.color }"
        >
        </div>
        <button
            class="button"
            :class="{ disabledButton: !inStock }"
            :disabled="!inStock"
            v-on:click="addToCart"
        >
          Add to cart
        </button>
      </div>
    </div>
  </div>
</template>