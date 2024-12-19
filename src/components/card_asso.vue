<template>
  <div class="cards-container">
    <div class="card">
      <h3 class="card-title">Avant l’adoption</h3>
      <p class="card-text">
        Simplifiez les démarches d’adoption et trouvez les foyers idéaux grâce à des outils
        intuitifs.
      </p>
    </div>
    <div class="card">
      <h3 class="card-title">Pendant l’intégration</h3>
      <p class="card-text">
        Suivez chaque adoption de près et anticipez les besoins des adoptants avec un tableau de
        bord dédié.
      </p>
    </div>
    <div class="card">
      <h3 class="card-title">En cas de difficultés</h3>
      <p class="card-text">
        Accompagnez les adoptants dans chaque étape pour garantir une intégration réussie et éviter
        les retours en refuge.
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
// Pas de logique dans ce composant pour l'instant
</script>

<style scoped>
.cards-container {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  justify-content: center;
  padding: 1rem;
}

/* Style des cartes */
.card {
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  max-width: 300px;
  width: 100%;
  min-height: 215px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;

  h3 {
    font-size: 1.25rem;
    font-weight: 600;
    margin: 0.5rem 0;
    color: #333;
    line-height: 1.5; /* Ajustez pour un meilleur espacement */
  }

  @media (max-width: 768px) {
    h3 {
      line-height: 1.3; /* Plus compact sur les petits écrans */
    }
  }
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
}

/* Image dans la carte */
.card-image {
  width: 100%;
  height: auto;
  border-radius: 8px;
  margin-bottom: 1rem;
}

/* Titre de la carte */
.card-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: #333;
}

/* Texte de la carte */
.card-text {
  font-size: 0.95rem;
  color: #666;
  margin-bottom: 1rem;
  line-height: 1.5;
}

/* Bouton de la carte */
.card-button {
  background: #007bff;
  color: white;
  border: none;
  border-radius: 25px;
  padding: 0.5rem 1rem;
  cursor: pointer;
  font-size: 0.9rem;
  transition:
    background-color 0.3s ease,
    transform 0.2s ease;
}

.card-button:hover {
  background: #0056b3;
  transform: scale(1.05);
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .cards-container {
    flex-direction: column;
    align-items: center;
  }

  .card {
    max-width: 90%;
  }
}

@media (max-width: 480px) {
  .card-title {
    font-size: 1.1rem;
  }

  .card-text {
    font-size: 0.85rem;
  }

  .card-button {
    padding: 0.4rem 0.8rem;
    font-size: 0.8rem;
  }
}
</style>
