<template>
    <label for="">
        <input type="checkbox" @change="onChange" name="" id="" >
        {{ label }}
</label>
</template>


<script setup>

defineProps({
    label:  String
});

 const emits = defineEmits(['check', 'uncheck']);
const onChange = (event) => {
    if(event.currentTarget.checked)
    {
        emits('check', event.currentTarget);
    }else{
        emits('uncheck', event.currentTarget);
    }
}

</script>