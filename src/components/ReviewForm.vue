<script setup>
import { ref } from 'vue'

const emit = defineEmits(['review-submitted'])

const name = ref('')
const review = ref('')
const rating = ref(null)
const recommend = ref(null)

const onSubmit = () => {
  if (name.value === '' || review.value === '' || rating.value === null) {
    alert('La revue est incomplète. Veuillez remplir au moins le nom, le commentaire et la note.')
    return
  }


  let productReview = {
    name: name.value,
    review: review.value,
    rating: rating.value,
    recommend: recommend.value
  }

  emit('review-submitted', productReview)


  name.value = ''
  review.value = ''
  rating.value = null
  recommend.value = null
}
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Laissez un commentaire</h3>

    <label for="name">Nom:</label>
    <input id="name" v-model="name">

    <label for="review">Commentaire:</label>
    <textarea id="review" v-model="review"></textarea>

    <label for="rating">Note:</label>
    <select id="rating" v-model.number="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <div class="radio-container">
      <label>Recommanderiez-vous ce produit?</label>
      <div>
        <input type="radio" id="yes" value="Oui" v-model="recommend">
        <label for="yes">Oui</label>
        <input type="radio" id="no" value="Non" v-model="recommend">
        <label for="no">Non</label>
      </div>
    </div>

    <input class="button" type="submit" value="Valider">
  </form>
</template>

<style scoped>
.review-form {
  display: flex;
  flex-direction: column;
  padding: 20px;
  margin: 20px 0;
  border: 1px solid #ddd;
}
.review-form label {
  margin-top: 10px;
}
.review-form textarea {
  height: 80px;
  resize: none;
}
.radio-container {
  margin-top: 15px;
}
.radio-container div {
  display: flex;
  gap: 10px;
  margin-top: 5px;
}
</style>