<template>
  <button @click="showTimer = !showTimer">Afficher / Masquer Timer</button>
  <Timer v-if="showTimer" />

  <form @submit.prevent="addTodo">
    <fieldset role="group">
      <input v-model="newTodo" type="text" placeholder="Tâche à faire">
      <button :disabled="!newTodo.trim()" type="submit">Ajouter</button>
    </fieldset>
  </form>

  <div v-if="todos.length === 0">
    Vous n'avez aucune tâche à faire
  </div>

  <div v-else>
    <ul>
      <li v-for="todo in sortedTodo" :key="todo.date">
        <label>
          <input type="checkbox" v-model="todo.completed">
          <span :class="{ completed: todo.completed }">{{ todo.title }}</span>
        </label>
      </li>
    </ul>

    <label>
      <input type="checkbox" v-model="hideCompleted">
      Masquer les tâches complétées
    </label>

    <p v-if="remainingTodos > 0">
      {{ remainingTodos }} tâche{{ remainingTodos > 1 ? 's' : '' }} à faire
    </p>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import Timer from './Timer.vue';
import Button from './Button.vue';
import Layout from './Layout.vue';

const newTodo = ref('');
const hideCompleted = ref(false);
const todos = ref([]);
const showTimer = ref(true);

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    todos.value = data.map(todo => ({
      title: todo.title,
      completed: todo.completed,
      date: todo.id
    }));
  } catch (error) {
    console.error('Erreur lors du chargement des tâches :', error);
  }
});

const addTodo = () => {
  if (!newTodo.value.trim()) return;
  todos.value.push({
    title: newTodo.value.trim(),
    completed: false,
    date: Date.now()
  });
  newTodo.value = '';
};

const sortedTodo = computed(() => {
  let sorted = todos.value.slice().sort((a, b) => a.completed - b.completed);
  return hideCompleted.value ? sorted.filter(t => !t.completed) : sorted;
});

const remainingTodos = computed(() => todos.value.filter(t => !t.completed).length);
</script>

<style>
.completed {
  opacity: 0.5;
  text-decoration: line-through;
}
</style>
