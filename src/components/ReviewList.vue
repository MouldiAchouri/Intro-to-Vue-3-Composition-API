<script setup>
defineProps({
  reviews: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <div class="review-container">
    <h3>Commentaires:</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        {{ review.rating }} étoiles (⭐️) par {{ review.name }}
        <br/>
        "{{ review.review }}"
        <br/>
        Recommande: **{{ review.recommend }}**
        <hr/>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.review-container {
  padding: 20px;
  border: 1px solid #ddd;
  margin-top: 20px;
  background-color: #f9f9f9;
}
.review-container ul {
  list-style-type: none;
  padding: 0;
}
.review-container li {
  padding: 10px 0;
}
.review-container hr {
  border: 0;
  border-top: 1px dashed #ccc;
  margin: 10px 0;
}
</style>