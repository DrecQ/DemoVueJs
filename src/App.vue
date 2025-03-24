<template>
  <p> Compteur : {{ count }} </p> 

  <button @click="increment">Incrémenter</button>
  <button @click="decrement">Décrémenter</button>

  <!-- Affichage des films -->
   <ul>
     <!-- Boucle pour afficher chaque film -->
     <li v-for="movie in movies" :key="movie"> {{ movie }}  <button @click="deleteMovie(movie)">Supprimer</button> </li>
   </ul>

</template>

<script setup>
  import { ref } from "vue";

  // Création d'un ref pour stocker le compteur
  const count = ref(0)

  //Creation d'un tableau 

  const movies = ref([
    'Matrix',
    'Inception', 
    'Eternal Sunshine of the Spotless Mind', 
    'Pulp Fiction', 
    'The Dark Knight', 
    'The Godfather',
  ])



  // Méthodes pour augmenter et diminuer le compteur
  const increment= () => {
    count.value++
  };

  const decrement= () => {
    count.value--
  };

  // Méthode pour supprimer un film
  const deleteMovie = (movie) => {
    movies.value = movies.value.filter(m => m!== movie)
  };
</script>

