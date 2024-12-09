<script setup>
   import Button from 'primevue/button';
   import InputText from 'primevue/inputtext';
   import {ref, defineEmits } from 'vue'

   const newTask = ref('')

   const emit = defineEmits(['handleAddNewTodo']);
    const addNewTodo = () => {
      emit('handleAddNewTodo', {name: newTask.value}); // Emit with parameter
      newTask.value = ''
    };

</script>

<template>
   <div class="container">
     <InputText class="input" v-model="newTask"/>
     <Button label="Add" @click="addNewTodo" severity="success" />
   </div>
</template>

<style>
  .container {
    margin-bottom: 10px;
    display: flex;
    justify-content: space-between;
    width: 100%;
    gap: 10px;
  }

  .input {
    width: 100%;
  }
</style>
