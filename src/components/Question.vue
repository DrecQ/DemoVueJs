<template>
    <div class="question">
        <h3> {{ questions.question }}</h3>

        <ul>
            <li v-for="(option, index) in randomChoices" :key="option">
                <Answer :id="`answer${index}`" :disabled="hasAnswer" :value="option" v-model="answer"
                :correctAnswer="questions.answer"/>
            </li>
        </ul>
        <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button>
    </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue';
import { shuffleArray } from './functions/array';
import Answer from './Answer.vue';

const props = defineProps({
    questions : Object
});

const emits = defineEmits(['answer']);
const answer = ref(null);
const hasAnswer = computed(()=> answer.value !== null);
const randomChoices = computed(()=> shuffleArray(props.questions.options));
</script>

<style>
   .question {
        padding-top: 1rem;
    }

    .question button
    {
        margin-left: auto;
        display: block;
    }
</style>