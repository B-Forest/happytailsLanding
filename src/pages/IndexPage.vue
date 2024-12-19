<template>
  <div class="background">
    <div class="content">
      <h1>🐾 Happy Tails</h1>
      <p>
        Garantissez une adoption réussie et durable grâce à un accompagnement interactif et
        personnalisé, renforcé par un suivi fiable et proactif des professionnels de la SPA, pour
        assurer le bien-être de l’animal et la satisfaction des adoptants.
      </p>
      <form class="form">
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
        <div class="buttons">
          <button
            type="button"
            class="btn btn-association"
            @click="handleSubmit('Je suis une association')"
          >
            🏢 Je suis une association
          </button>
          <button
            type="button"
            class="btn btn-adopter"
            @click="handleSubmit('Je souhaite adopter dans le futur')"
          >
            🐶 Je souhaite adopter dans le futur
          </button>
        </div>
      </form>
      <p v-if="successMessage" class="success-message">
        <i class="icon fa fa-check-circle"></i> {{ successMessage }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
import { Notify } from 'quasar'

const email = ref('')
const successMessage = ref('')
const errorMessage = ref('')

const validateEmail = (email: string) => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return emailRegex.test(email)
}
const handleSubmit = async (buttonContent: string) => {
  try {
    if (!validateEmail(email.value)) {
      alert('Veuillez entrer une adresse email valide.')
      return
    }
    const response = await axios.post('https://api.bforestdev.fr/files/write', {
      email: email.value,
      content: buttonContent, // Envoi du contenu (texte)
    })

    if (response.status === 201 || response.status === 200) {
      // Notification de succès
      Notify.create({
        message: 'Email et contenu envoyés avec succès !',
        color: 'green', // Couleur verte pour le succès
        position: 'top', // Positionnement de la notification
        timeout: 3000, // Durée avant que la notification disparaisse
      })

      successMessage.value = 'Email et contenu envoyés avec succès !'
      email.value = '' // Vide le champ email après l'envoi
    }
  } catch (error) {
    console.error("Erreur lors de l'envoi :", error)

    // Notification d'erreur
    Notify.create({
      message: "Une erreur est survenue lors de l'envoi.",
      color: 'red', // Couleur rouge pour l'erreur
      position: 'top',
      timeout: 3000,
    })

    errorMessage.value = "Une erreur est survenue lors de l'envoi."
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

.background {
  position: relative;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 4rem 2rem;
  font-family: 'Poppins', sans-serif;
  color: black;

  &::before {
    content: '';
    background-image: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.3)),
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

.content {
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  max-width: 600px;

  h1 {
    font-size: 2.8rem;
    margin-bottom: 1rem;
    color: $primary;
    font-weight: 600;

    @media (max-width: 768px) {
      font-size: 2rem;
    }
  }

  p {
    font-size: 1.2rem;
    margin-bottom: 1.5rem;
    color: #555;
    line-height: 1.6;

    @media (max-width: 768px) {
      font-size: 1rem;
    }

    @media (max-width: 480px) {
      font-size: 0.9rem;
    }
  }

  .form {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1.5rem;

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

    .buttons {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: center;
      gap: 1rem;

      .btn {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 0.5rem;
        padding: 0.8rem 1.5rem;
        font-size: 1rem;
        font-weight: bold;
        border: none;
        border-radius: 25px;
        cursor: pointer;
        color: white;
        transition:
          background-color 0.3s ease,
          transform 0.2s ease;

        &:hover {
          transform: scale(1.05);
        }

        &.btn-association {
          background-color: $primary-second;

          &:hover {
            background-color: $primary;
          }
        }

        &.btn-adopter {
          background-color: $secondary-second;

          &:hover {
            background-color: $secondary;
          }
        }
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

/* Responsive adjustments */
@media (max-width: 768px) {
  .content {
    padding: 1.5rem;
  }

  .buttons .btn {
    font-size: 0.9rem;
    padding: 0.6rem 1.2rem;
  }
}

@media (max-width: 480px) {
  .content {
    padding: 1rem;
  }

  .buttons {
    flex-direction: column;
    gap: 0.8rem;

    .btn {
      width: 100%;
    }
  }
}
</style>
