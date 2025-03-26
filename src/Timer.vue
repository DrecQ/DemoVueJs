<template>
    <div>
        Temps : {{ time }}
    </div>
</template>


<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

let timer; 

const time = ref(0);

onMounted(() =>{
    timer = setInterval(() => {
        time.value++;
    }, 1000); 
});

onUnmounted(() =>{
    clearInterval(timer);
});


</script>