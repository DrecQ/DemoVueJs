<template>
    <label :for="id" :class="classes">
        <input :disabled="disabled" type="radio" name="answer" :id="id" v-model="model"  :value="value" />
        {{ value }}
    </label>
</template>

<script setup>
import { computed } from 'vue';

 const props = defineProps({
    id : String,
    disabled : Boolean,
    value : String,
    correctAnswer : String,
 })

 const model = defineModel()

 const classes = computed(() =>{
    right: props.disabled && props.value === props.correctAnswer
 })
</script>

<style>
.right
{
    color: green;
}
</style>