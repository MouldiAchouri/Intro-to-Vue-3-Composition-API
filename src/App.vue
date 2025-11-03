<script setup >
import {ref} from 'vue'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const productImage = socksBlueImage
const inventory = 10
const onSale = ref(true)

</script>

<template>
<div class="product-display">
    <div class="product-container">
      <div class="product-info">
        <h1>Socks</h1>
      <p v-if="inventory > 10">En stock</p>
      <p v-else-if ="inventory >= 1 && inventory <=10 ">faible stock</p>
      <p v-else> rupture de stock</p>
      <p v-show="onSale">En Solde !</p>
      </div>
    </div>
  </div>
</template>