<template>
  <p :style="{color: count  > 5 ? 'red' : 'green' }">
    Compteur : {{ count }}
  </p> 

  <div v-show="count >= 5">Bravo, vous avez atteint 5 clics</div>
    <button @click="increment">Incrémenter</button>
    <button @click="decrement">Décrémenter</button>

</template>

<script setup>

  import { ref } from "vue";
  const count = ref(0)

  const increment= () => {
    count.value++
  };

  const decrement= () => {
    count.value--
  };

</script>

