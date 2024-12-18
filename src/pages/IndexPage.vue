<template>
  <div class="background">
    <div class="content">
      <h1>Happy Tails</h1>
      <p>
        Garantissez une adoption réussie et durable grâce à un accompagnement interactif et
        personnalisé, renforcé par un suivi fiable et proactif des professionnels de la SPA, pour
        assurer le bien-être de l’animal et la satisfaction des adoptants.
      </p>
      <form @submit.prevent="handleSubmit" class="form">
        <input type="email" placeholder="Votre email" class="email-input" required />
        <div class="buttons">
          <button type="button" class="btn btn-association">Je suis une association</button>
          <button type="button" class="btn btn-adopter">Je souhaite adopter dans le futur</button>
        </div>
      </form>
      <p v-if="successMessage" class="success-message">{{ successMessage }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'

const email = ref('')
const successMessage = ref('')

const handleSubmit = async () => {
  try {
    const response = await axios.post('http://localhost:3000/submit', { email: email.value })
    if (response.status === 200) {
      successMessage.value = 'Email envoyé avec succès !'
      email.value = '' // Vide le champ après l'envoi
    }
  } catch (error) {
    console.error("Erreur lors de l'envoi :", error)
  }
}
</script>

<style lang="scss">
.background {
  position: relative;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: start;
  color: black;
  text-align: center;
  padding: 10rem;

  &::before {
    content: '';
    background-image: url('/pictures/bg_picture.jpg');
    background-size: cover;
    background-position: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0.5;
    z-index: -1;
  }
}

.content {
  position: relative;
  z-index: 1;

  p {
    margin-bottom: 20px;
    font-size: 1.2rem;
    font-weight: 500;
    color: #333;
    padding: 0 10rem;
  }
}

h1 {
  margin-bottom: 20px;
  font-size: 3rem;
  color: #333;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

.email-input {
  padding: 10px 15px;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 300px;
  outline: none;
}

.buttons {
  display: flex;
  gap: 10px;
}

.btn {
  padding: 10px 20px;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  color: white;
  transition: background 0.3s ease;

  &.btn-association {
    background-color: #007bff;

    &:hover {
      background-color: #0056b3;
    }
  }

  &.btn-adopter {
    background-color: #28a745;

    &:hover {
      background-color: #1e7e34;
    }
  }
}
</style>
