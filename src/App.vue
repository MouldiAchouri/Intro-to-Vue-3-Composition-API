<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'
 
const product = ref('Socks')
const details = ref(['50% coton', '30% laine', '20% polyester'])
const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage },
  { id: 2235, color: 'blue', image: socksBlueImage }
])
 
const sizes = ref(['S', 'M', 'L', 'XL'])
const image = ref(socksGreenImage)
function updateImage(variantImage) {
  image.value = variantImage
}
</script>
 
<template>
  <div class="product-display">
    <div class="product-container">
 
      <div class="product-info">
        <h1>{{ product }}</h1>
 
        <h3>Composition :</h3>
        <ul>
          <li v-for="(item, index) in details" :key="index">{{ item }}</li>
        </ul>
 
        <h3>Couleurs :</h3>
        <div style="display: flex; gap: 20px;">
          <div v-for="variant in variants" :key="variant.id" style="text-align: center; cursor: pointer;" @click="updateImage(variant.image)">
            <p>{{ variant.color }}</p>
            <img :src="variant.image" :alt="variant.color" style="width: 80px; height: auto; border: 1px solid #ccc; border-radius: 8px;">
          </div>
        </div>
 
        <h3>Tailles :</h3>
        <div style="display: flex; gap: 10px;">
          <span v-for="(size, index) in sizes" :key="index" style="border: 1px solid #ccc; padding: 5px 10px; border-radius: 5px;">
            {{ size }}
          </span>
        </div>
 
      </div>
    </div>
  </div>
</template>