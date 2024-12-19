<template>
  <div class="background">
    <div class="content">
      <h1>🐾 Happy Tails</h1>

      <!-- Toggle -->
      <div class="toggle">
        <button :class="{ active: userType === 'adoptant' }" @click="userType = 'adoptant'">
          🐶 Je suis un adoptant
        </button>
        <button :class="{ active: userType === 'asso' }" @click="userType = 'asso'">
          🏢 Je propose l'adoption
        </button>
      </div>

      <!-- Dynamic Components -->
      <component :is="activeComponent" />

      <p class="little-text">
        Si vous êtes intérrésé renseigner votre email pour que l'on puisse vous contacter
      </p>
      <form class="form" @submit.prevent="handleSubmit">
        <div class="input-wrapper">
          <input
            type="email"
            placeholder="Votre email"
            v-model="email"
            class="email-input"
            required
          />
          <i class="icon fa fa-envelope"></i>
        </div>
        <button type="submit" class="btn btn-submit">Envoyer</button>
      </form>

      <p v-if="successMessage" class="success-message">
        <i class="icon fa fa-check-circle"></i> {{ successMessage }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import axios from 'axios'
import { Notify } from 'quasar'
import CardAsso from 'components/card_asso.vue'
import CardAdopt from 'components/card_adopt.vue'

// State
const email = ref('')
const userType = ref('adoptant') // "asso" or "adoptant"
const successMessage = ref('')

const activeComponent = computed(() => (userType.value === 'adoptant' ? CardAdopt : CardAsso))

// Form Handling
const validateEmail = (email: string) => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return emailRegex.test(email)
}

const handleSubmit = async () => {
  try {
    if (!validateEmail(email.value)) {
      alert('Veuillez entrer une adresse email valide.')
      return
    }
    const buttonContent =
      userType.value === 'adoptant' ? 'Je suis un adoptant' : "Je propose l'adoption"

    const response = await axios.post('https://api.bforestdev.fr/files/write', {
      email: email.value,
      content: buttonContent,
    })

    if (response.status === 201 || response.status === 200) {
      Notify.create({
        message: 'Email envoyé avec succès !',
        color: 'green',
        position: 'top',
        timeout: 3000,
      })
      successMessage.value = 'Email envoyé avec succès !'
      email.value = '' // Reset email field
    }
  } catch (error) {
    console.error("Erreur lors de l'envoi :", error) // Utilisation de la variable
    Notify.create({
      message: "Une erreur est survenue lors de l'envoi.",
      color: 'red',
      position: 'top',
      timeout: 3000,
    })
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

.background {
  position: relative;
  display: flex;
  height: 100vh;
  justify-content: center;
  align-items: flex-start;
  text-align: center;
  padding: 1.5rem 2rem;
  font-family: 'Poppins', sans-serif;
  color: black;

  &::before {
    content: '';
    background-image: linear-gradient(
        to bottom,
        rgba(0, 0, 0, 0.3),
        rgba(0, 0, 0, 0.3),
        rgb(255, 202, 155)
      ),
      url('/pictures/bg_picture.jpg');
    background-size: cover;
    background-position: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
  }
}

/* Pour les tablettes */
@media (max-width: 768px) {
  .background {
    height: 100%; /* Ajustez cette valeur selon vos préférences */
  }
}

.content {
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  padding-top: 0;
  padding-bottom: 1rem;
  min-height: 625px;

  h1 {
    font-size: 2.8rem;
    margin: 1rem 0;
    font-weight: 600;
    color: $primary;
  }

  p {
    font-size: 1.2rem;
    margin-bottom: 1.5rem;
    color: #555;
    line-height: 1.6;
  }

  .little-text {
    font-size: 1rem;
    color: #666;
    margin-bottom: 1rem;
  }

  .form {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;

    .input-wrapper {
      position: relative;
      width: 100%;
      max-width: 400px;

      .email-input {
        width: 100%;
        padding: 0.8rem 3rem 0.8rem 1rem;
        font-size: 1rem;
        border: 2px solid #ccc;
        border-radius: 25px;
        outline: none;
        transition: border-color 0.3s ease;

        &:focus {
          border-color: $primary;
        }
      }

      .icon {
        position: absolute;
        right: 10px;
        top: 50%;
        transform: translateY(-50%);
        font-size: 1.2rem;
        color: $primary;
      }
    }

    .btn-submit {
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 25px;
      padding: 0.8rem 1.5rem;
      font-size: 1rem;
      cursor: pointer;
      transition: background-color 0.3s ease;

      &:hover {
        background-color: #218838;
      }
    }
  }

  .toggle {
    display: flex;
    justify-content: center;
    margin-bottom: 1rem;
    gap: 1rem;

    button {
      padding: 0.8rem 1.5rem;
      border: none;
      border-radius: 25px;
      font-size: 1rem;
      cursor: pointer;
      background-color: #ccc;
      color: #fff;
      transition: background-color 0.3s ease;

      &.active {
        background-color: $primary;
      }
    }
  }

  .success-message {
    margin-top: 1.5rem;
    font-size: 1.1rem;
    color: #28a745;
    font-weight: bold;

    .icon {
      margin-right: 0.5rem;
    }
  }
}
</style>
