<template>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input v-model="newTodo" type="text" placeholder="Tâche à faire" id="">
      <button :disabled="newTodo == 0" type="submit">Ajouter</button>
    </fieldset>
  </form>
 <div v-if="todos.length == 0"> Vous n'avez aucune tâche à faire </div>

 <div v-else>
  <ul>
    <li v-for="todo in sortedTodo()" :key="todo.date" :class="{completed: todo.completed }">
      <label for="">
        <input type="checkbox" v-model="todo.completed" name="" id="">
        {{ todo.title }}
      </label>
    </li>
  </ul>

  <label for="">
      <input type="checkbox" name="" v-model="hideCompleted" id="">
        Masquer les tâches complétées
  </label>
 </div>
</template>

<script setup>
import { ref } from 'vue';

const newTodo = ref('')

const hideCompleted = ref(false)

//Tableau des taches 
const todos = ref([
  {
    title: 'Tâche test',
    completed: true,
    date: 1,
  },
  {
    title: 'Autre tâche',
    completed: false,
    date: 2,
  }
]);

const addTodo = () => {
  todos.value.push(
    {
      title: newTodo.value,
      completed: false,
      date: Date.now(),
    }
  );

  newTodo.value = '';
}

//Methode ^pour trier le tableau

const sortedTodo = () =>{
  const sortedTodo = todos.value.toSorted((a,b) => a.completed > b.completed  ? 1 : -1);

  if(hideCompleted.value == true)
  {
    return sortedTodo.filter(t => t.completed == false);
  }

  return sortedTodo;

}

</script>


<style>
  .completed
  {
    opacity: .5;
    text-decoration: line-through;
  }
</style>
