<template>
  <div class="container">
    <div v-if="state === 'error'">
      <p>Une erreur s'est produite lors du chargement des données.</p>
    </div>

    <div v-else-if="state === 'loading'">
      <p>Chargement en cours...</p>
    </div>

    <div v-else>
      <Quiz :quiz="quiz" v-if="quiz"/>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import Quiz from './components/Quiz.vue';

// Variables
const quiz = ref(null);
const state = ref('loading');

// Charger les données
onMounted(async () => {
  try {
    const response = await fetch('/Quiz.json');
    if (!response.ok) {
      throw new Error('Impossible de charger les données');
    }
    quiz.value = await response.json();
    state.value = 'idle';
  } catch (error) {
    console.error(error.message);
    state.value = 'error';
  }
});
</script>
